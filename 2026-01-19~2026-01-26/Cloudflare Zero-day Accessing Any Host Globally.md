> For educational purposes only. Summarized on Jan 24, 2026.

# Cloudflare Zero-day: Accessing Any Host Globally

## Summary
The write-up tells the story of how traffic aimed at that certificate path could reach origins behind Cloudflare even when the rest of the application was blocked by customer rules, why that matters, how we proved it with restraint, and how the issue is fixed.

We were reviewing access posture on a set of applications where the WAF was configured to block the world and only allow specific sources. Everywhere else, the WAF did exactly what it said on the tin. But when we pointed a request as ```/.well-known/acme-challenge/{token},```, the WAF stepped aside and the origin answered with its own voice.

On the demo hosts, we used small, idempotent* requests and appended a harmless suffix to the token (for example, ```/ae```) to show that no real ACME file was required for the behavior to appear. In every case, we received origin responses where we should have been meeting the WAF.

WAF controls are meant to be the front door. When a single maintenance path bypasses that door, the definition of inside moves. In practical terms, the trust boundary for ```/.well-known/acme-challenge/...``` slid from the WAF to the origin. Once the origin is addressable from the internet - even for one route - ordinary bugs acquire a network path and ordinary pages become reconnaissance.

On Spring and Tomcat, using a well known traversal quirk in some servlet stacks(```..;/```), the request could land on ```/actuator/env``` and return process environment and configuration. That data often includes sensitive values - database URLs, API tokens, cloud keys - and it materially raises the blast radius of any mistake in the origin.

On Next.js, server side rendering frameworks routinely ship server derived values to the client in order to hydrate the page. That is fine when the WAF owns the front door. When the origin answers directly, the same page can expose operational details that were never intended to be reachable from the public internet.

On PHP, many PHP apps route all request through ```index.php``` and use a query parameter to select a view. When that pattern carries an LFI bug, public reachability turns it into a file read. Asking for ```../../../../etc/hosts``` is enough to demonstrate the impact. In our demo, even the 404 flow was routed through ```index.php```, which is why it surfaced additional pages once the origin began to speak directly.

\* It means that performing the same action multiple times has the same effect as doing it once.

## Note

### ACME
ACME is the protocol that lets certificate authorities verify domain control. In the HTTP-01 method, the CA expects your site to serve a one-time token at ```/.well-known/acme-challenge/{token}```. The CA fetches that token over plain HTTPS like any other client would; if the bytes match, the certificate is issued. The intention is strict and minimal: let the bot read a small file at a very specific path, and nothing more.

### HTTP-01
HTTP-01 is the most common challenge type used by the ACME protocol to prove domain ownership. It relies on the simple principle that only the legitimate owner of a domain can host specific content on that domain’s web server. When a certificate is requested, the CA provides a unique token, and the server must place it in a publicly accessible directory. While effective, its reliance on a predictable path (/.well-known/acme-challenge/) often leads WAF providers to create "allow-list" exceptions.

### LFI (Local File Inclusion)
LFI is a critical vulnerability that occurs when an application includes a file without properly validating its path. This allows an attacker to manipulate input - often through "dot-dot-slash" (../) sequences - to trick the server into exposing sensitive files stored locally, such as /etc/passwd or configuration logs.

## Tag
\# Cloudflare \# WAF \# Vulnerability \# Patched

## Reference
https://fearsoff.org/research/cloudflare-acme