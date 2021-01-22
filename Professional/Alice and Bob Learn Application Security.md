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
- 

**What can I do with this?**
- What actions am I going to take based on this book, if any?

**Personal Bottom Line**
- x/10
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTcwNjMwNDUwNCwtMTAyMzk4NDU3MywyMD
QyMTgwNjc1LC05OTY4MjM3MDIsLTIwMjk3NjQ1NzUsLTE1Mzg3
OTU3MTddfQ==
-->