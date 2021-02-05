## A Philosophy of Software Design

**Purpose For Reading**
- Highly rated, was in the book club, always looking for design perspective.
 
**Main Takeaways & Metacognition**
- Two goals:
	- Describe what complexity is and why it matters
	- Present techniques to reduce it.
- Complexity = anything that makes code hard to understand or change.
	- "If you write a piece of code and it's simple to you but complex to others, it's complex."
	- Complexity causes "Change amplification," which means you have to change code in many different places often.
	- Complexity requires more "Cognitive load," which is how much a developer needs to know in order to do something to the code.
- Basically, the most important thing you can do is try to be obvious and clean.
- Tactical vs. Strategic programming:
	- Tactical programming: Doing the least amount of work to get a job done.
		- Sometimes "pros" at this are mislabeled as heroes when all they're doing is leaving tons of technical debt behind that someone else will have to repay.
	- Strategic programming: "Working code isn't enough." Primary objective is to produce a great design that also happens to work.
		- How much to invest? Spend 10-20% on investing in good design.
- "Depth"
	- Modules (classes / services / etc) should minimize dependencies between each other. They have an interface and an implementation.
	- Interfaces should be SIMPLE. Don't show unimportant stuff. LESS IS BETTER.
	- Implementations should have lots of functionality.
	- WHAT YOU WANT: Small, simple interfaces with implementations that offer lots of functionality. These two together = "Deep modules".
	- DON'T WANT: Shallow modules whose interface is complicated relative to the functionality they provide.
		- "Classitis"
- "Information hiding": Modules should hide complexity in them rather than pass them to whoever's using them through the interface. e.g., things like retry logic.
	- Pull complexity DOWN into implementation. Don't let it float up to interfaces.
- "Temporal Decomposition:" the bad design approach of designing code structure based on execution order.
- Make classes general purpose. An interface should be general enough to support multiple uses.
	- Ask yourself: What's the smallest / simplest interface I could create?
- Design red flags:
	- Layers of abstraction that don't line up.
	- Pass-through methods.
	- Using decorators (an object extends another object to extend its functionality). Why not add it to the base class?
	- Pass-through variables that are used through chains of methods. Try using a context object instead, particularly for things like configuration.
	- Dividing up classes too much. If two classes overlap conceptually, share information, are used together frequently, or don't make sense without looking at each other, combine them.
	- Don't split up methods unless it actually makes the system simpler. Not a problem to have long methods. Each method should do one thing, completely.
- Exceptions / errors: THROWING EXCEPTIONS EVERYWHERE IS LAZY. Can you really not handle the cases internally? If so, do it, don't make it the issue of the person using your interface.
	- Maybe you can ignore them entirely.
	- Sometimes just crashing is OK if it makes sense.
- Design things twice. Every time. Going with your gut is rarely the best solution. This is hard, and you are not stupid. Take the time.
- Comments:
	- Pretty straightforward. Make them readable, don't overuse them, use good and descriptive variable names, use them at different levels.
	- GENERAL GOAL: Comments should document information on the designer's mind that can't be reflected in code, or things that aren't obvious.
	- Keep comments close to the code they're for.
	- Write your comments BEFORE your code, not after.
	- No obvious place for your comment? Create a "DesignDecisions.md" file in your code, write your comment, and reference it.
- Naming:
	- Take your time and come up with great names.
	- Shouldn't be more than two or three words.
	- Be PRECISE
	- Be CONSISTENT
	- If it's hard to name the variable, then re-think your design, because it probably isn't clean / obvious.
- Modifying existing code? Continue to develop strategically. Don't just make the system work (tactically). Refactor if it makes sense.
- Much more important for code to be READABLE than easily writable.
- Writing for performance: Make code simple. Don't "if" everywhere.

**What can I do with this?**
- "DesignDecisions.md"
- In general, I like the idea that making your system obvious is a great thing to prioritize in design. I'll probably look at my code in a new light.

**Personal Bottom Line**
- 8/10
- Nothing groundbreaking, good reinforcing concepts.
- A lot of fluff with the examples, BUT they were very easy to skip over.
- Not sure I agree with the takes on TDD not being desirable because it restricts design.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY0MzEzNjcwLC01MTU1NTI4MDhdfQ==
-->