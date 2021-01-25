## Alice & Bob Learn Application Security

**Purpose For Reading**
- From the Liazon Book Club
- Haven't read a security-centered book in a few years at least, good time for a refresher.
- Probably add some good stuff to my cheat sheet project.
 
**Main Takeaways & Metacognition**
- **Chapter 1 - Security Fundamentals**
- Security boils down to CIA:
	- Confidentiality (my data isn't visible)
	- Integrity (data is current, correct, accurate)
	- Availability (up and running)
- "Assume Breach": design with the assumption that someone has access to the network.
	- Things should be locked down.
	- Access everywhere should be monitored and logged.
- "Coordinated disclosure": announcing a vulnerability AFTER there's been enough time to patch it.
- "Insider threats": saboteur employees, or employees who could possibly screw CIA up by accident.
- "Defense in depth": Concept that multiple layers of security is good. e.g., Secure Coding + Security Testing + Firewall + Door locks and keypads in the server rooms.
- "Least privilege": Only grant the access that is absolutely necessary so that if someone were to get your access they can only do limited damage.
- "Supply chain security": In software, concept is that you have to carefully monitor your code dependencies for vulnerabilities.
	- "Modern applications are typically made up of 20-40% original code, with the rest being third-party components."
- "Security by obscurity": Concept that hiding sensitive information is a layer of security in itself. It's not complete BS but also usually isn't a legit strategy on its own.
- "Attack surface reduction": removing everything from the application that isn't completely required. e.g., don't broadcast SSID of WiFi.
- "Never trust, always verify" anything and everything outside of the application. Validate data, validate permissions. Re-check on different pages.
- "Usable security": There's a balance between good security and usability. Extreme end of scale: Never putting your application on the internet. Pragmatic: Fingerprint readers, passphrases that are easier to remember than passwords.
- "Authentication Factors": DOES NOT JUST MEAN TWO PASSWORDS. Basically means check for multiple FORMS of authentication:
	- Something you HAVE: e.g., a phone token, a computer that's been validated...
	- Something you ARE: fingerprint, iris scan, DNA...
	- Something you KNOW: Password, pass questions
- So "MFA" would actually mean you can use a phone authenticator AND a password, but just using a password and pass questions doesn't count because they're the same form of auth.
- **Chapter 2: Security Requirements**
- "Partnership model": Assigning a security person to a development team, typically during a project kickoff.
- Questions to ask during requirements gathering / analysis:
	- Any PII?
	- Where and how are we storing data?
	- Is the app available publicly or internally only?
	- Is the app doing anything sensitive or essential (e.g., moving money, unlocking doors, delivering medicine)
	- Does the app do anything risky, e.g. allow users to upload files?
	- What availability do we need?
	- Etc.
- **ENCRYPTION**
	- "Cryptography": math that can be applied to information in order to make its value no longer understandable.
	- "Encryption": Two-way cryptography. You encrypt, send something, and the receiver can decrypt.
	- "Hashing": ONE-WAY cryptography. You can never get back to the original value. USED FOR PASSWORD STORAGE.
	- In general, encrypt in transit (sending data) and at rest (storing in database).
- NEVER TRUST SYSTEM INPUT.
	- "System input" is literally anything and everything that isn't part of your application. e.g., user input, info from _your own database_, info from APIs, URL parameters, cookies, images, HTTPS request headers, web proxies, config files...
	- "XSS": JavaScript injected into your application from a hacker's browser. **Defeated by output encoding**, which would show "<script...." on the screen rather than run code on the user's browser.
- Writing a new low-level program? Use Rust. It's memory safe, unlike C++ / C.
- Use a third-party tool to scan your components for vulnerabilities.
- **SECURITY HEADERS**
	- Generally set these in the web app / server.
	- Content-Security-Policy: explicitly defines what sources for contents are allowed for images, scripts, etc, so that nothing else will run. Can also define a report-uri that will log what was blocked.
	- X-Frame-Options: prevents other sites from being able to put yours in a html frame that could dupe users.
	- X-Content-Type-Options: tells the browser not to guess the content type of media in the app.
	- Referrer-Policy: Sets how much of the URL another web app can see if your user navigates away. e.g., "www.blah.com" instead of "www.blah.com/user/23523", or nothing at all.
	- Strict-Transport-Security (HSTS): forces the connection to use HTTPS. Must have a certificate from a Certificate Authority (CA) installed.
	- Feature-Policy: Basically turn off access to HTML 5 features like gyroscopes, ambient lite sensors, vr. Only allow what your site uses.
	- X-Permitted-Cross-Domain-Policies: Literally Adobe-specific (Flash, Reader). Set it to "none".
	- Expect-CT: CT = Certification Transparency, which is an open agreement that builds consensus on how legit CAs are. If on, the browser will check the CT to make sure your cert is legit.
	- Public Key Pinning Extension for HTTP (HPKP): a system created to protect against fraudulent certs, BUT it's very risky to have one because it can break the site unless you know what you're doing. Not recommended.
- **Securing cookies**
	- DO NOT USE PERSISTENT COOKIES THAT ARE SAVED. Only use session cookies, which are stored in RAM.
	- These settings are all for the Set-Cookie header.
	- Set-Cookie: Secure; // ensures that cookies are only sent over HTTPS
	- HttpOnly: ensures that cookies can't be accessed by JavaScript. Only from the server. This protects against XSS attacks that try to access values in the cookie.
	- Persistence: Anything that doesn't self-destruct at the end of a session is considered a persisted cookie. You can set a date or a maximum age here.
	- Domain: If you want your cookie to be accessed by other domains, list them here.
	- Path: limit access to the cookie to a specific path on your app. Good for scenarios where your app is huge and divided up.
	- Same-Site: based on CSRF ("Sea-surf"), Cross-Site Request Forgery protection. Where an attacker tries to take actions on the user's behalf. This attribute ensures that cookies can only come from within the same site.

**What can I do with this?**
- What actions am I going to take based on this book, if any?

**Personal Bottom Line**
- x/10
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzQ5MTQ1MjQ4LC0xNDk5NzI3OTM0LC0xMj
QwMjE5MDI2LDIwNTU2ODM4MTEsLTg3NTUyMTk5MSwxOTM5ODEy
ODkyLDYyMDUxNzU1NiwtMTk0OTEwOTg3OSwtMTc0MDU3MTQ3OC
wtMTEzNTc2OTc5NywtMTI3NDM2MjU5NCwtMTAyMzk4NDU3Mywy
MDQyMTgwNjc1LC05OTY4MjM3MDIsLTIwMjk3NjQ1NzUsLTE1Mz
g3OTU3MTddfQ==
-->