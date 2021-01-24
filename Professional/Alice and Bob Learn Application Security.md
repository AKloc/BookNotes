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

**What can I do with this?**
- What actions am I going to take based on this book, if any?

**Personal Bottom Line**
- x/10
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkyODY1ODk2LDE5Mzk4MTI4OTIsNjIwNT
E3NTU2LC0xOTQ5MTA5ODc5LC0xNzQwNTcxNDc4LC0xMTM1NzY5
Nzk3LC0xMjc0MzYyNTk0LC0xMDIzOTg0NTczLDIwNDIxODA2Nz
UsLTk5NjgyMzcwMiwtMjAyOTc2NDU3NSwtMTUzODc5NTcxN119

-->