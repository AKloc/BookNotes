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

**- Chapter 3: Secure Design**
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

**On Backups:**
	- They aren't valuable unless you can roll them back efficiently.
	- Have to be stored in geographically different locations, securely.
	- Schedule rollback practices.
	- DB, configs, AND code need to all be backed up.
	- Monitor and log backup access.

**Server Side Security Validation**
	- Test using a web proxy / intercept proxy (a tool that sits between your browser and the web server, intercepting traffic and interacting with the application directly)
	- This testing helps ensure that you aren't just relying on your front end for validation.

- Always use framework security tools instead of trying to home-grow it.
- Whenever possible, isolate security functionality from other functionality. e.g., put input validation in a separate object / class, put authn and authz in separate applications, use your cloud provider's IM tool.
- Identiy and authn should live on a separate server.
- Partition your application - especially system management / admin.
- Secrets: Humans should never see them except when they're being updated or in case of emergency. Integrate into CI/CD.
- CSRF is when an attacker gets a user to click a link that triggers a transaction to an application the user is already logged in on (so they're "surfing" on the user being logged in). Avoid it asking the user something only they could provide before doing anything important or by using anti-CSRF tokens.
- Separate out production data.
- Protect your code.
- Threat modeling is good.
	- Good place to start: create "evil" user stories / abuse stories.
	- Popular models to start with: STRIDE and PASTA. 
	- Once you have a good list of concerns, evaluate how much damage they could do and how easy they are to pull off. 
	- Then decide what you're going to do. Fix or migrate? Ignore? Document it.

- **Chapter 4 - Secure Code**
- If you want your engineers to use secure practices, you have to support them actively.
- (Really good input flow validation diagram on page 89)
- Actively disable any HTTP verbs you're not using.
- AUTHN = Authentication - validates you are who say you are.
- AUTHZ = Authorization - validates you're allowed to do what you're trying to do.
- "Access Control" = the system that manages AUTHZ.
- Use a pre-made Auth system, e.g. OAUTH.
- Session Management:
	- Track session using a session ID or a session token. They're the same thing. They get passed in secure cookies, are at least 128 characters long, and randomized. Users get a new session ID each time they login.
	- Use built-in session management, don't homegrow it.
	- Make sure sessions expire.
	- Only send the session ID over encrypted channels.
	- Destroy the session when a user logs out.
	- If a session ID is sent that was never generated, LOG IT in SEIF. It's a security incident.
- Bounds checking: Buffer overflows. If you're using a language that's susceptible, be wary.
- Permission Types for access control:
	- Discretionary Access Control (DAC): the owner of the info / system / resources can grant and remove access to others.
	- Mandatory Access Control (MAC): Grants access to information and systems based on the SENSITIVITY level of the resource and the user. e.g., Bob has top-secret access, Alice doesn't. Bob can't grant Alice access like he'd be able to do with DAC.
	- Permission Based Access Control (PBAC): Uses permissions like Read / Write / Create / Update / Delete / Print / Reboot / Etc

- ** Chapter 5 - Common Pitfalls **
- OWASP Top Ten is handy for learning. They have a few projects like the ZAP proxy and Proactive Controls.
- Defend against CSRF, which is where an attacker gives a link to do something bad to a user who's already logged in.
	- Reverify the user is who they say who they are.
	- Confirm with the user that they want to do big operations.
	- Ensure that the referrer header from the request is from the site, and not from another site or email address.
- Defend against SSRF, where an attacker modifies / adds URL parameters sent to a server to try to do things they shouldn't be able to.
	- Don't use URL parameters where possible.
	- Validate inputs using approved / accelpted lists.
	- Create an approved list of domains that are permitted for each call. Reject anything else.
	- Use request filtering, which is typically a feature of your tech stack.
	- Disable unused URL schemas (file:///, dict:///, ftp://, etc)
- Don't do deserialization in general. Use JSON / XML / YAML / etc instead.

- **Chapter 6 - Testing and Deployment **
- Static Testing: "Testing" code itself. Doesn't have to be running.
- Dynamic Testing: Testing the code when it's actually running.
- SAST: Static Application Security Testing. 
	- Generally provide a lot of results that can be false positives, but should be waded through.
	- List of free and paid tools at owasp.org/www-community/Source_Code_Analysis_Tools
- SCA: Software Composition Analysis. Automates analysis of the components your application is using to assess risk, security, and license compliance.
	- Can be helpful if not just to document a "Software Bill of Materials" that lists all of the components your system uses.
	- List of paid and free tools: owasp.org/www-community/Component_Analysis#tools-listing
- IAC: Infrastructure as code. Generally a great thing for security, since it's very helpful with change management (view the diffs in a repository), Disaster Recovery, and eliminates things like humans forgetting steps or mistyping configuration.
- Web Proxies: Great for testing well-known vulnerabilities like injection, XSS, etc. Lets you mess with the data being sent directly to the application.
- Fuzzing: Send invalid, unexpected, or generally garbage to the system and see what happens. Do things crash? Does it fail elegantly?
	- Check Urls, APIs, input fields, cookies, headers... any inputs.
- VA / Security Asessment / PenTests: Hire security professionals to try hacking the system and report their findings. 
	- Can be used to shock and awe management if they don't "get" security.
- Security Hygeine: Verifying that your applications are following your policies and standards.
	- Check crypto. There are free tools that will look at your crypto settings and give recommendations around things like the length of ciphers, the type of encryption being used, etc.
	- Check security headers and cookie settings.
	- Free tools: securityheaders.com, hardenize.io, SSL Labs.
	- SAST (Static App Security Testing) tools can also help.
	- Some of these checks can be automated and put into a CI / CD pipeline.
- IAST: Interactive Application Security Testing. Basically an AI / ML agent that sits in your system, monitors it, and reports vulnerabilities.
	- Advised to use this in a pre-prod environment.
- Database Testing / Validation:
	- Each account should only be able to access certain things.
	- You shouldn't be able to connect to the server without an account.
	- Close off all ports except what's needed for operation.
	- Don't install any other software on the DB server.
	- All data should be classified and labeled - is it secret / top secret / unclassified?
	- No service accounts have dbo.
	- Data is encrypted in transit and at rest.
	- DNS resolution on the server is internal-only.
	- Etc.
- Testing APIs:
	- Start with a good request, then start sending bad ones.
	- Try using every HTTP verb and see if they work.
	- Test field length limits.
	- Send stuff like "<script>" and see if the server takes it.
- Testing Networks:
	- Close every port.
	- Only service accounts should be able to access APIs / DBs / etc.
- Deployment:
	- Add checks to CI/CD, but RESPECT DEV AND OPS's time limits. If you slow them down too much it will ultimately undermine your work.
	- Example checks: Scan the code delta between last release and current result for anything that looks like a secret. Run a software composition analysis against the delta to ensure no one added a sketchy package.

** Chapter 7 - An AppSec Program **
- AppSec: A program (not software) of security-minded, long-term activities to keep your software secure.
	- Do we perform threat modeling on each design?
	- Do we check for security considerations at PRs? How?
	- The program is FORMALIZED. They're official, mandatory. No one skips or takes shortcuts.
- AppSec goals: Some use OWASP, SAMM, BSIMM as a starting point and tweak from there.
- Create an Application Inventory that has all of your APIs, databases, applications, assets, etc. 
- 

**What can I do with this?**
- What actions am I going to take based on this book, if any?

**Personal Bottom Line**
- x/10
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4NjI1MjM0NDQsMTMwMzk0NDg4OSwtMT
gyNTUzNTc2NCw5MDk5NzY4NzMsMTAzODg0MTczMSwtODgzMDcx
OTU1LC05NDQ1NTY3OTIsMTU4OTY1OTUxNiwxMDk1OTIyMTQsMT
E0NDk4NjYxMywtMTIxOTk4OTQwNCwxOTE0MTMyODUwLC0xNTEw
MTY2OTA1LC0xMDc5MjM2NTk0LC0yNzk2NzM5OTgsLTEyMzE3NT
g5NDYsLTE0OTk3Mjc5MzQsLTEyNDAyMTkwMjYsMjA1NTY4Mzgx
MSwtODc1NTIxOTkxXX0=
-->