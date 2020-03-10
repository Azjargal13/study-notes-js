# General questions#1

Difference between cookies, session storage and local storage?

resources are from:
-

# Cookie

- The very first time user sends request to the server and establish connection, it stores the tokens or session data, which only can be read by server side (means stored in the server). Generally cookies are used with HTTPOnly cookie flag.
- Cookies are not accessible through Javascript
- Immune to XSS
-  Can be set secure cookie flag to guarantee the cookie is sent over HTTPS
-  when Cookies are primary for reading `server-side`. Apart from being an old way of saving data, cookies can give 4096 bytes per cookie.
-  vulnerable to CSRF (Cross Site Request Forgery)
-  Cookie can only be sent to the domains in which it is allowed.
- Cookies have expiry data.
- Persistent data but data is unencrypted.
# Local storage
- can only be read by the `client-side` (means it is stored in client side storage). 
- local storage is an implementation of the `Storage` interface, its limit is as big as 5MB per domain. It stores data with `no expiration date` and gets cleared only through Javascript or clearing Browser Cache/Locally stored data. (stored directly in the browser)
- local storage or web storage is accessible through JS on the same domain.
- vulnerable to XSS (cross site scripting) attack
- in order to prevent XSS, the common response is to escape and encode all untrusted data. 
- companies and organizations are advised not to store anything of value or trust any information in web storage. This includes session identifiers and tokens.
- web storage does not enforce any secure standards during transfer. Whoever reads web storage and uses always send JSON Web Token (JWT) over HTTPS, not HTTP.

# Session storage
- Non persistent data storage
- scoped only current window, means until the tab closes the stored data is available in current open window. (stores something temporarily)
- session storage is an implementation of the `Storage` interface.