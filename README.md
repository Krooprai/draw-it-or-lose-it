# draw-it-or-lose-it
CS-230-week-7

# CS 230 Journal 

Repository artifact: Software Design Document 
Draw It or Lose It (The Gaming Room)

## Reflection Questions

#Briefly summarize The Gaming Room client and their software requirements. Who was the client? What type of software did they want you to design?

The client was The Gaming Room, a company that owned an existing Android only game called Draw It or Lose It. They wanted CTS to redesign the game as a platform independent, web-based application that could reach Mac, Windows, Linux, and mobile users from a single code base instead of separate native builds. Their core technical requirements were that only one instance of the game management service could exist at a time, that game and team names had to be unique, and that a game's drawing and guessing rounds run on permanent time windows (30 seconds and 15 seconds) enforced regularly for every connected player.

#What did you do particularly well in developing this documentation?

I think the strongest part of the document is how directly the design decisions trace back to the client's stated requirements. Every pattern I chose has a clear reason tied to a requirement instead of being picked for its own sake the Singleton pattern for GameService exists certainly because the client needed one authoritative source of game state, and the Iterator pattern in addGame(), addTeam(), and addPlayer() exists specifically to enforce the uniqueness requirement. That traceability made the document easier to defend and easier to extend later, including when I added the Recommendations section for the operating platform, storage, memory, distributed systems, and security.

#What about the process of working through a design document did you find helpful when developing the code?

Writing the Design Constraints section before writing any code forced me to think through concurrency and network reliability issues up front like multiple users trying to claim the same team name at once instead of discovering them mid-implementation. Documenting the domain model as a UML diagram before coding also clarified the inheritance relationship between Entity and Game, Team, and Player, so when I did write the Java classes, the structure was already settled and I wasn't redesigning relationships in the middle of implementation.

#If you could choose one part of your work on these documents to revise, what would you pick? How would you improve it?

I would go back and flesh out the Evaluation section comparing Mac, Linux, Windows, and mobile as development and deployment targets. In the final document I made a clear recommendation in the Recommendations section, but the earlier Evaluation table could have done more legwork to justify that choice by comparing concrete tradeoffs licensing cost, available development tooling, and server stability side by side across platforms, instead of leaving that reasoning mostly for the Recommendations section to carry on its own.

#How did you interpret the user's needs and implement them into your software design? Why is it so important to consider the user's needs when designing?

I treated each requirement the client stated single code base across platforms, unique names, one authoritative game state, timed rounds as something the design had to satisfy explicitly rather than something to keep in mind loosely. That's why the domain model uses plain Java with no Android specific dependencies, why GameService is a Singleton, and why every add method checks uniqueness before committing a new record. Considering user needs this closely matters because a design that's technically elegant but doesn't map back to what the client actually asked for creates rework later or worse, ships something the client can't use. Anchoring every design decision to a specific requirement is what let me explain and justify the design to a non-technical stakeholder.

#How did you approach designing software? What techniques or strategies would you use in the future to analyze and design a similar software application?

I approached it by starting from the client's requirements and constraints, then moving to a domain model, and only after that to specific design patterns rather than picking patterns first and trying to justify them afterward. In future projects, I want to keep using that same order: capture requirements and constraints explicitly, model the domain with a UML diagram before writing code, and choose design patterns based on which specific requirement each one solves. I'd also want to build out the platform/technology evaluation earlier in the process, since that comparison work turned out to be just as useful for justifying later architecture decisions as the domain model itself was.

