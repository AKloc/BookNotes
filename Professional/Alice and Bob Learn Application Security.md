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
	- Cookie Prefixes: Ensures that if you're using subdomains, that your cookies only work in the subdomains they're assigned to using the host prefix.
- **Passwords**:
	- Password managers = good. Particularly, they defend well against credential stuffing (e.g., adding the number at the end of your password by 1 because of password expirations)
	- "Rainbow credential stuffing": Using variations of stolen passwords.
- ** Secret Stores**:
	- Basically password managers for computers. A software vault that encrypts secrets and allows an application to access them programmatically (e.g., Azure app variables)
	- Service accounts: Accounts used by computers, not people.
-  **Storing Passwords**
	- Stored in a database, salted and hashed.
	- Salting: Adding a long, unique value to a password BEFORE you hash it to increase entropy. The salt is stored alongside the password and is preferably more than 30 characters.
	- Hashing: A ONE WAY cryptographic process. You never want to decode the original password.
	- General flow: User punches in their password to log in. The system takes the password, adds the stored salt for that user, and then runs the password through the encryption scheme. It gets back an ugly string, which is compared to what's in the database.
	- "Work factor": basically how many times you run the hashing algorithm. Adds entropy.
	- "Peppering": Similar to a salt, but the pepper is used for every user in the system AND it's stored in a secret store rather than alongside the hashed password in the database. Basically considered extra credit and not necessary for most applications.
	- Don't force users to change passwords unless you suspect an actual breach.
	- Make sure users passwords haven't been used already.
	- Use a service like HaveIBeenPwned to make sure the password wasn't in a breach.
	- If a user enters bad credentials, never indicate if it was a bad username or a bad password.
	- Use a modern hashing algorithm.
- **HTTPS Everywhere**:
	- Only be accessible through HTTPS. If someone tries HTTP, reroute to HTTPS.
	- Use the latest TLS.
- **File Uploads**:
	- Always extremely dangerous.
	- Use a third-party component that specializes in them.
	- OWASP has a great list of precautions to take on their cheatsheetseries.
- Errors and Logging: use a SIEM.
	- SIEM:  "Security Incident and Event Management System" to collate all errors and logs in one place.
- **Input Validation and Sanitization **:
	- Have to do it on the server side.
	- Where possible, make a list / use a regex and define what's allowed, and reject everything else.
- Authorization / Authentication: Use RBAC, and figure out how you're going to define roles during requirements.
- Parameterized Queries = stored procedures. Use them because they don't allow SQL injection.
- URL Parameters: Don't put any variables in the URL that are too important. Don't use IDs that can be incremented to find someone else's info.

**Chapter 3: Secure Design**
- Design Flaw: An error in the design that lets a user do something they shouldn't be able to do.
- Security bug: An implementation issue that lets a user do something they shouldn't be able to do.
- In general: The further you can push security left and design with it in mind from the beginning, the cheaper.

**- For all data:**
	- Encrypt in transit.
	- Encrypt at rest.
	- Use HTTPS only.
	- Valide inputs.
	- Encode outputs.
	- Use security headers.
	- Don't put sensitive information in hidden fields or URL parameters.
	- Secure cookies (use session cookies as much as possible)
	- Use RBAC to ensure users have auth to get to data at each endpoint.
	- Plan on how long the application is required to store data and plan on how to get rid of it.
	- If geographically distributed, decide where data and backups will be stored.
	- Hash and salt passwords. Pepper if required.
	- Create alerts if any data is leaked online that looks like your data. US: www.us-cert.gov/ncas/alerts
	
**Never trust. Always verify. Zero trust. Assume breach.**
	- Anything foreign input should be tested at the server.
	- Deny access by default and require authorization, even on individual page reloads.
	- Fail closed or safe (e.g., go back to a default page). Roll back transactions that fail midway.
	- Authenticate, then authorize.
	- Block access to any protocol, port, HTTP verb that isn't used.
	- One application per server / PaaS / container / etc.

**- On Backups:**
	- They aren't valuable unless you can roll them back efficiently.
	- Have to be stored in geographically different locations, securely.
	- Schedule rollback practices.
	- DB, configs, AND code need to all be backed up.
	- Monitor and log backup access.

** Server Side Security Validation **
	- Test using a web proxy / intercept proxy (a tool that sits between your browser and the web server, intercepting traffic and interacting with the application directly)
	- This testing helps ensure that you aren't just relying on your front end for validation.



**What can I do with this?**
- What actions am I going to take based on this book, if any?

**Personal Bottom Line**
- x/10
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NjY4Mzc1MDYsLTg4MzA3MTk1NSwtOT
Q0NTU2NzkyLDE1ODk2NTk1MTYsMTA5NTkyMjE0LDExNDQ5ODY2
MTMsLTEyMTk5ODk0MDQsMTkxNDEzMjg1MCwtMTUxMDE2NjkwNS
wtMTA3OTIzNjU5NCwtMjc5NjczOTk4LC0xMjMxNzU4OTQ2LC0x
NDk5NzI3OTM0LC0xMjQwMjE5MDI2LDIwNTU2ODM4MTEsLTg3NT
UyMTk5MSwxOTM5ODEyODkyLDYyMDUxNzU1NiwtMTk0OTEwOTg3
OSwtMTc0MDU3MTQ3OF19
-->