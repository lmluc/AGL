# AGL

Interview suggestions from Jon Embury:
In terms of the overall process, I like something along the lines of:

A) Initial informal chat, phone or in-person. Ask a couple of basic questions to vet.
B) Have the candidate come in for a formal interview. Interviews for techies should always involve writing or analysing some code on a whiteboard.
C) If passed that interview, decision point. For juniors / intermediates, I'd suggest we hire at this point if we're confident they can grow. For senior and above, I would prefer to assign a short home work question to be responded to as working code. This creates the additional internal workload to review it, but means we get to look at coding style, choices and trade offs, comments, etc.

Example coding problems for during-interview:

Super Basic:
* Reverse the order of this string of characters: {A,B,C,D,E} - any approach is fine, you look for corner case errors - empty array, duplicate value being dropped errors.
* Order of this series of numbers: {A,B,C,D,E} - any approach is fine, bonus points for bubblesort or quicksort implementations, but those have been pretty rare in my experience.

Slightly harder:
* Provide the sum of an array of numbers, looking for implementation approach, errors on negative numbers and zeros.
* Find the duplicates in an array of numbers

Harder:
Given a customers billing history, work out the rolling 2-year average quarterly bill as of the last billing period, every 3 months. - Provide a list of example transactions and dates. For bonus points, use intermediate result caching with on-demand re-calculation (for the purposes of the question, in-memory cache over multiple runs is fine).

Take home

Harder / Longer
* https://briangordon.github.io/2014/08/the-skyline-problem.html - I quite like this one for data engineers / FP people, because it's essentially implementing a version of a map / reduce type approach. While some candidates will have seen it before, that's not a bad sign - and it's fairly straight forward to alter it slightly to get around the google-an-answer question, e.g. make it the ice-berg problem and turn it upside down. It took me about 1.5 hours to write a simple solution in C# from a cold start. 

Very Hard - unlikely to use, but fun to think about.
Operating systems - Demonstrate how to implement a forced flush to disk from cache in Linux by implementing a kernel timer, free choice of file system.FP 
Data / Programming - Demonstrate how to convert ANSI SQL to SparkQL or MapReduce jobs using a compiler / pre-compiler.

Interviews Questions - 
Here's some of the common questions I ask techies, I try to keep these technology agnostic and vary based on experience, the danger being that they trend academic and need to be carefully worded. 

OS fundamentals - There's a goldmine of fundamental CS questions to be derived from https://www.bottomupcs.com/ 
* Explain mutual exclusion?
* What's the difference between a thread and a process in Liunx (or any *nix)
* What's the difference beween protected and user memory?

Networking:
What's a port in IP? / Explain what a bitmask is for? Explain how IP routing tables work?

More practical / experience based questions:
* Explain idempotent service design?  - more useful with integration types, looking for answers which demonstrate an understanding of state management.

* What's the difference between a hash-map and an array? - Looking for an understanding and consideration of access efficiency vs. problem at hand.

* Define ACID properties of a database - more for traditional data base people, many will have forgotten the overall meanings but muddle through. Looking for a clear understanding of transactions, isolation and concurrency in databases. If the candidate can't get all the way though, I fall back on something like:

* Explain the difference between optimistic and pessimistic locking?
  
* What's the CAP theorem (https://en.wikipedia.org/wiki/CAP_theorem), or a variant of the question - not many people will recognise the question as it's not well taught, but most experienced IT people have an implicit learned understanding of the implications. If candidate doesn't recognise the term I usually give the definitions and ask them to explain the trade offs and implications. This question is very useful with solution architecture and distributed systems people, as you're looking for an understanding of the trade offs in different design choices.

Hard - * Describe the travelling salesman problem (https://simple.wikipedia.org/wiki/Travelling_salesman_problem), and possible solutions - only to be used when dealing with strong computer science backgrounds / outside edge question

Programming:
In OO - The usual explain classes, inheritance, polymorphism, generics, overloading, singleton implementations, etc. For bonus points, explain the fragile base class problem (https://en.wikipedia.org/wiki/Fragile_base_class)
In functional programming, define immutability, explain case classes (Scala), how do you approach refactoring functional code?
Runtime fundamentals for JVM / .NET CLR - What's garbage collection / what's a generational garbage collector / What's the heap?

As you move up the technology experience scale, I like to add in "compare and contrast" type questions, e.g.:

For OO programmers - Compare two languages on your resume - what are the pros and cons each way?
For functional guys - Which problem sets are suited or not suited to functional approaches, how do you choose your tools?
For DBAs - What are the major differences and decision points between n different platforms you've used?, e.g. When do you use Teradata or similar, and when do you use HDFS? etc. 

What I'm looking for here is rational judgement based on problem characteristics and consideration of the context of the solution - the business, the support teams, the available engineering teams, rather than ideology-first answers. This has worked well for me from senior techs through solution architects. 

re: Discussion yesterday, I have a volunteer to look at a couple of Scala responses for us to get started, but I don't want to stretch the friendship too far.....

Let me know if this helps, or if you need elaboration on the questions / example code.

Additional homework question suggestion - Implement a thread pool (without using the runtime constructs that are supplied). 

Generally, most engineers will use the built in implementations without great consideration as to how they work, but it's a good indicator of ability to deal with a multi-threaded / multi-host application.

Basically, you need to build three things:
* A container for some threads
* A way of creating threads to fill it as needed
* A way of acquiring / assigning work, and recovering the threads afterwards (post completion or error)

And for the purposes of the exorcise:
* Some work to do
* A throughput limit to ensure the pool reaches exhaustion
* Occasional failure.

Let's call it the checkout problem - you have 1000 people waiting in line, you have 10 check outs. Build a system to represent the scenario, where each checkout processes as many of the customer's baskets as possible, records the total of the basket and cash collected from customers and reports on the cash position of the til at the end of the day. Each basket contains randomly contains 1-5 items, with random prices between $0.05 and $500. Each checkout processes one customer at a time, all 10 are open.

Extension 1: 10% of customers (randomly selected) have an item with no price, which needs a price check, which causes the check out process to abort, and pass the customer to a manual / secondary queue for processing.

Extension 2: A check-out operator gets ill, and walks off the job, ensure the system continues to process all customers. This may happen while a customer is being served.

Build a simulation of the system described, language is players choice.

