## DevOps For Dummies (December 2020)

**Purpose For Reading**
- Book club pick, has come up before in conversations of good books.
 
**Main Takeaways & Metacognition**
- DevOps is way bigger than CI/CD.
- SDLC = "Software DELIVERY Life Cycle". Like that idea.
- Be DELIBERATE about culture. Don't let it be run by inertia.
- Values:
	- Encourage teamwork
	- Reduce silos
	- Practice systems thinking (everything impacts everything)
	- Embrace failure
	- Communicate
	- Accept feedback
	- Automate processes when appropriate
- "Values are meaningless if you don't incentivize the behavior that lives up to them."
	- Idea prizes
	- Hack time
	- Fun off-sites
- Gartner's Hype Cycle
- **Conceiving a new product**
- Discovering the problem the MVP should solve:
	- What is the challenge you want to solve?
	- Why does the challenge exist?
	- In which industry is it most commonly experienced?
	- Does the problem affect the majority of people or is it niche?
	- If you're the customer, why do you need this product?
	- What's the value of solving this problem?
- "If your company has no competitors, that's a huge red flag."
	- Who are my competitors' customers?
	- Is my MVP in line with theirs?
	- How is my MVP differentiated?
	- How can I steal customers or reach customers?
- Bucket features into three categories to start drawing up a roadmap:
	- Features you can't live without
	- Features that are nice to have
	- Features that don't matter (basically items that no one would fight for)
- Create customer personas, deliberately.
	- Have to understand and be able to project your perspective users.
	- Create four or five INDIVIDUALS. With names, jobs, genders, salaries, locations. Build using these individuals as a lens.

**Back to DevOps Stuff**
- Document architecture decisions, including why you DON'T do certain things, in a .md file called "Architecture Decisions" in the code.
- Keep people in marginalized groups at least in pairs so they can amplify each other's voices rather than feel isolated.
- "Mushroom Management": Devs get limited information based on manager decisions alone, with no collective understanding.
- Deployment Schemes:
	- Blue-green: Deploy new release to another environment and then move all traffic over at once.
	- Canary: Same as blue-green, but rather than moving everything at once between environments, send canary groups over to make sure they don't have issues.
	- BOTH REQUIRE THAT YOU CAN MANAGE YOUR SESSIONS ACROSS ENVIRONMENTS.
- Measures to watch when trying to improve performance on page 171.
- "Dogfooding": Using your own software.
- "Wouldn't you be loyal to an organization that took a risk on you? Wouldn't you be excited to work hard?
- MOTIVATION:
	- Autonomy
	- Mastery
	- Purpose
- Post-incident questions on page 257
- HTTP Response codes on page 283. Nice little breakdown.
	- 200: "It's all good"
	- 300: "Go here for what you're looking for"
	- 400: "User error."
	- 500: "It's me, not you."

**What can I do with this?**
- I have to use "inertia" more.
- Why do we not have a "How was your experience" box when users finish enrollment?
- Great employee poll questions on page 66. I like the idea of giving a free-form textbox after each question
- Add a field to feature tickets for business objectives? Which client are we landing... WHY are we doing this?
- The MVP questions on page 86 are concise and probably a good copy / paste for some side projects.


**Personal Bottom Line**
- x/10
- Really well-written, good pacing.
- Content is definitely broader than what I thought would be, but not in a bad way. Good insights with some of the culture stuff and how it all ties together.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA5MzAzMDIyMywxOTM0NzExNzI3LC03Mz
AwNzU0MTcsMzU2NDI3OTcsLTEyNDM3MDA4MDEsLTgwODUzNzU5
NCwxNDY3NDcwNDEsLTE1MTIyODA3MDEsLTc3NTg3MDA4OCwxNj
A0ODE3NjE1LDI3MzI2MDgyMCw4MjE5ODA0NzNdfQ==
-->