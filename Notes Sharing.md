#Shared Notes

If you know html feel free to reformat and push to github

TLDR [3]: A Model of Computer Systems
===

**CPU:** The brain. It does the actual computing.

+ Each type of computer has its own machine language. 

**RAM:** Technically called random access memory, aka. the main memory.
+ contains sequence of locations, locations are numbered by address

**Fetch & Execute Cycle:** fetch instruction from memory then carry out or execute the instruction

**Registers:** Small memory units capable of holding a single number or machine language instruction. 

**PC:** Program Counter
+ Keeps track of where in the program it is executing.
+ CPU checks PC to see which instruction to fetch

**Interrupts:** A signal sent to the CPU by other devices.
+ Forces the CPU to stop what its doing and accept input. 
+ Ex. Key press.

**Interrupt Handler:** Handles incoming interrupts and passes them to the CPU
+ The handler is used to enable efficient asyncronous computing
+ The handling process is as follows:
    + Saves the current computation state into memory
    + responds to interrupt
    + then jumps back to previous memory location

**Process:** Individual tasks that the CPU completes.

**Threads:** Processes may consist of multiple streams of execution. ??

**Preemptive multitasking:** Sending interrupts to all currently running threads at regular intervals.
+ Forcibly suspends threads that are taking too long.
+ Modern laptops and smartphones use this.

**Programmers:** You.
+ They write event handlers, so that they don't have to deal with interrupts directly

**Machine language:** A language that consists of very simple instructions that can be executed directly by the
CPU of a computer.

**Compiler:** translates high level programming language into machine language

**Interpreter:**  translates it instruction-by-instruction, as necessary.

**Virtual Machine:**

**Software Engineering:** The construction of correct, working, well-written programs. 
*(Not being part of the unwashed masses)*

**Top-down programming:** The design philosophy of breaking down large problems 
into smaller problems until the problems are small enough to solve.
+ Deals entirely with instructions (doesn't adequately consider data that program manipulates)
+ Difficult to reuse work

**Bottom-up Design:** The design philosophy of starting with problems you know how to solve
 *(reusable software)*, and building ontop of the smaller pieces like lego until you have a 
  complete solution.
+ Reusable software should be modular
+ This philosophy uses information hiding to ensure easy updation in the future without having
  to track down any misuses of private information.

**Module:** A component of a larger system that interacts with the rest of the 
system in a simple, well-defined, straight-forward manner.

**Object:** A structure *(module)* for organizing the following:
 + Information *(data)* 
 + Analysis tools *(methods)*


###edited to here completely
##TLDR [4]: A Brief History of a Program
**Steps to compile:** The compiler does the following when you hit the compile button: 
   + Evaluates high level language *(Python, Java, C, etc.)* humans can *(mostly)* understand using:
      + Analysis
          +
      + Parsing
          +
   + Convert to assembly language
     + Ex. For Intel i5 processor
       + Obtain binary file.
    
**Steps to run:**
 + Load binary file using operating system *(clicking run/double click app/enter from command line)*
 
**Where is the result stored?**
+ At a memory address
+ At a offset address from a base address (base address is created at runtime)
 
**Stack *(region of memory)*:** Where local variables declared in a function are stored. Keeps track of functions running in a program.
 
**Heap *(region of memory)*:** data whose sizes cannot be known ahead of time (at compile time) are stored on the heap. Arrays are stored in heap (so that it can grow in size)
 
**Program Counter (PC):** where program instructions are stored.
 
**Stack frame:** created to support the function’s execution. 
+ Contains function's local variables and the arguments passed to the function by its caller. '
+ contains housekeeping information that allows 
  + called function (the callee) to return to the caller safely. 
  + the address of the previous stack frame 
 
 
**Stack pointer:** points to top of stack. This is always changing, updated by CPU. Stack grows to lower memory addresses (local_buffer)

**Frame pointer:** fixed location within stack frame; stable reference point. Little CPU interference. Sometimes not needed, use compiler flags instead (Linux does this)

**Return value:** returns back to caller


7

##TLDR [5]: The Need for Specifications

**Preconditions:** conditions that exist before set of statements or
instructions are executed. 
+ Keyword: ***"requires"*** 
+ Ex. *(requires: val occurs in a)*
 
**Postconditions:** conditions that exist after. 
+  Keyword: ***"effects"*** 
+ *(effects: returns index i such that a[i] == va)*
 
**Frame conditions:** identifies which objects modified 
+ Keyword: "Modifies"
 
use preconditions and postconditions to reason about&debug programs
 
**Specification:** 
+ description of what an artifact does. 
+ 'contract' between producer(software developer) and user, described using pre, post conditions
+ Purpose: 
  + To improve understanding of the interface between two pieces of code.
    + Misunderstanding the interface between code results in bugs 
  + Different programmers may have different specifications
    + Decoupling the linkage between the client and the programmer aka 'firewall'.
      + Client doesn't have to know inner workings.
      + Implementer not affected by usage. 

**Why aren't specs **ALWAYS** used?:** we lazy. Limited time/money.
 
**Behavioural Equivalence:** when both give the functionality you want.  
 
**Source code is ambiguous** 
+ Which details of code’s behavior are essential? 
+ Which are incidental?
+ Code invariably gets rewritten.
+ Client needs to know what they can rely on.
+ What properties will be maintained over time?
+ What properties might be changed by future optimization, improved algorithms, or just bug fixes?
+ Implementer needs to know what features the client depends on, and which can be changed
 
**Static type declarations:** part of the PCPC of a method, automatically checked and enforced by the compiler. 
 
**Documentation comments:**  for what can't be written as types, duty of the user (Javadocs format: put postconditions in @return, preconditions&frame conditions in @param, @throw)
 
**Null:** *(for good programming)* disallowed as parameters and return values
 
**black box tests:** chosen with only the specification in mind, 
**glass box tests:** chosen with knowledge of the actual implementation
 
**Side effects:** when a method may return a value but also change the state of an object or datatype instance. 
 
**Mutation:** is disallowed unless stated otherwise
+	Strings are immutable
+	Arrays are mutable

tldr[6] Testing and Code Review

Validation: process of testing and code review, to uncover problems. Involves:
	- Verification: formal reasoning, proof
	- Testing: having inputs and checking results
	- Code review: someone else reason informally. 'proofreading'

residual defect rates: bugs left over after the software has shipped
Kloc: one thousand lines of source code

• 1 - 10 defects/kloc: Typical industry software.
• 0.1 - 1 defects/kloc: High-quality validation, java libraries
• 0.01 - 0.1 defects/kloc: Safety-critical, NASA and
Praxis. ~$1000 per line of code.

During programming: want it to work
Testers: want it to fail

Test early and often

Test-first-programming, "write tests first before code"
1. Write a specification for the function.
2. Write tests that exercise the specification.
3. Write the actual code.
Benefits: uncover buggy specs (incorrect, incomplete, ambiguous, missing corner cases)

Why is testing software hard?: 
	- Too many cases for exhaustive testing
	- Haphazard Testing less likely to find bugs (corner cases)
	- Random/Statistical Testing cannot test random sample (say, 1%) and infer 99% of the rest.

test suite: a set of test cases that cover different aspects of a program’s behaviour.
	- Small to run quickly
	- Enough to validate program
	1. divide the input space into subdomains
	2. Choose 1 input from each subdomain
	
Coverage of test suite: how thoroughly it 'exercises' the program
	- Statement coverage: is every statement run by some test case?
	- Branch coverage: for 'if', 'while' statement, true or false direction both taken
	- Path coverage: every path through program taken by test case

Bugs often occur at boundaries between subdomains
100% coverage is infeasible

Blackbox testing: choosing test cases only from the specification
Whitebox/glassbox testing: choosing test cases based on how function is implemented.

Regression testing: running all your tests after every change. New changes could introduce new bugs.
When you fix a bug, write a test case that elicits it.

Comments: 
Javadoc comment: starts with /** and
includes @-syntax, like @param and @return for methods.
Include specifications document assumptions.
Avoid direct transliterations of code into English

Summary

three techniques for reducing bugs:
• static checking
• testing
• code reviews

In testing, we saw these ideas:
• Test-first programming. Write tests before you write code.
• Partitioning and boundaries for choosing test cases systematically.
• White box testing and statement coverage for filling out a test suite.
• Automated regression testing to keep bugs from coming back.

In code review, we saw these principles:
• Don’t Repeat Yourself (DRY)
• Comments where needed
• Fail fast (might run, but not what you want)
• Avoid magic numbers
• One purpose for each variable (use final for method parameters, for variables (as many as you can). final says that the variable should never be reassigned)
• Use good names
• No global variables
• Coherent methods
• Return results, don’t print them
• Use whitespace for readability

Three C's - Correct - Comprehensible  - Changeable

tldr[7] Exceptions

Procedural specifications: help describe what method does & how clients should use the method
 
How should implementer handle exceptional situations, invalid inputs?
Ex. When you use find(x) and x does not occur, the return is -1. If the -1 is then used as an index for array, error. NOTE: find cannot return null because its return type is int
 
Exception construct: indicate problems, include techniques for clients to fix.
 
Method Signature: name, parameter types, return type, exceptions that may be triggered
 
Exceptions for Signalling Bugs: 
•	ArrayIndexOutOfBounds 
•	NullPointerException (when trying to call a method on null object)
•	ArithmeticException (division by 0)
•	NumberFormatException (cannot parse into format)
 
Exceptions for Special Results: 
If call method, and NotFound-Exception is not handled, compiler error
 
Java has 2 exception types: 
Unchecked: bugs, at runtime (error, runtimeException). only to signal an unexpected failure/if clients will not encounter exception. otherwise use checked.
Checked: special results, at compile time (throwable, exception). Must be caught.
 
Class hierarchy for Java exceptions
 
Throwable: class of objects that can be thrown or caught
 
Don't subclass Throwable or Error. Use RuntimeException
(to make it an unchecked exception) or Exception (to make it checked).
 
note that throws and throw is not the same



9
[8] How to Debug
systematic debugging practices: diagrams to represent memory states, reduce human misunderstanding
 
Primitive values: bare constants
 
Object values: circle labeled by its type
 
Mutable values: when assign to a variable or a field, you change variable's arrow points
 
Immutable "final" values:  variables that are assigned once, never reassigned. Strings. 
•	Final reference: DOUBLE ARROW
•	Final object: DOUBLE CIRCLE
 
StringBuilder: mutable object
 
Debug systematically:
1.	Reproduce the bug - small, repeatable test case.
2.	Localize (binary search) and understand the bug 
a.	Study data
b.	Hypothesis
c.	Experiment
d.	repeat
3.	Get help
4.	Swap components: are you implementing it correctly?
a.	java.util.ArrayList -> use injava.util.LinkedList instead. 
b.	binarySearch() -> linearSearch()
5.	Sleep on it
 
 
 
Summary
•	instance diagrams: difference between assignment and mutation.
o	objects represented by circles 
	a type and fields inside them
o	immutable objects, double border
o	a variable or field reference, an arrow
o	an immutable reference, a double arrow
systematic debugging:
•	reproduce the bug as a test case, and put it in your suite of tests (for later regression
tests);
•	find the bug using the scientific method;
•	fix the bug thoughtfully, and not as a short-term patch


[9] Avoid Debugging
1.	Make Bugs Impossible
2.	Localize Bugs
o	Assertions
o	What to Assert
o	What Not to Assert
o	Incremental Development
o	Modularity and Encapsulation
 
Make Bugs Impossible: 
•	Static checking @compile
•	dynamic checking (array overflow bugs)
 
Immutable reference variable: BUT the object may be mutable
 
Localize Bugs: 
Fail fast: detect early = closer to cause = easier to fix
 
Runtime assertions: 
•	tests preconditions (example of defensive programming), 
•	Indicates bugs
•	Write assertions as you write code
•	Is a built-in feature, 
•	but clutters code, so avoid trivial
•	executed only during testing and debugging.
o	Off when program released
•	are off by default in java
o	To enable: pass -ea (which stands for (which stands for enable assertions enable assertions) to the Java virtual machine. )
 
asset and asset.....() are different
•	Assert: for implementation code, defensive checks
o	Runs with -ea
•	Asset....() for JUnit tests, to check the result of a test
o	Will always run (without -ea)
 
What to assert: test the internal state of your program to ensure that it is within
the bounds of its specification. 
•	Method argument requirements
•	Method return value requirements
•	Covering all cases (below, vowels must be in listed cases, else fail)
 
What not to assert: 
•	assertions to test conditions that are external to your program,
o	The existence of files/the availability of the network/correctness of user input 
o	External failures are not bugs (no change you can make to your program in  advance that will prevent them from happening) Handle external failures with exceptions
 
Assertions can alter program, "side effects"
 
Incremental Development
Build program in chunks. Easier to identify where bug
 
Unit testing: test a module in isolation
Regression testing: when add feature to big system, run the regression test suite = in the code you just changed 
 
Modularity and Encapsulation 
 
Modularity: dividing system into components, or modules,
•	Each designed, implemented, tested, reasoned about, and reused
separately from the rest of the system. 
•	Note: opposite is monolithic system – pieces dependent on each other.
 
Encapsulation: building walls around a module = module is responsible for its own internal behavior = bugs in other parts of the system can't damage its integrity.
•	Access control: type of encapsulation: public and private to control
the visibility and accessibility of your variables and methods.
•	Variable scope: type of encapsulation: scope of a variable: portion of the program which variable is defined (expressions and statements can access). 
o	method parameter's scope is the body of method. 
o	local variable's scope is from declaration to the next closing curly brace.
 
Good Practice to:
•	Declare a variable when first used/in the innermost curly. Not all at start
•	Avoid global variables. 


[10] Designing Specs
Two types:
•	Operational specifications: give a series of steps that the method performs; pseudocode; descriptions are operational.
•	Declarative specifications: don't give details of intermediate steps;
give properties of the final outcome, and how it's related to the initial state.
 
We prefer declarative
 
If you want to substitute one method for another:
•	specification A stronger or equal to specification B if:
o	A's precondition is weaker
o	A's postcondition is stronger
•	Then, if implementation satisfies A, it will also satisfy B 
 
Domain: the set {int arrays X int s}
Range: all int s
 
What the definition doesn't capture: 
•	intend to return: integer for index in the array arr where we find val . 
•	If use binary search then arr must be sorted, method definition
does not capture this requirement.
 
We write method specifications 
•	(preconditions, postconditions, frame conditions) 
•	to more precisely define the domain (input set) and range (output set). 
•	So expectations (from method caller and implementer) are explicit
•	enables more careful reasoning about correctness
•	Useful for program decomposition
o	manage complexity
o	Implementer assumes preconditions are met
o	User assumes output is as expected
 
Comparing Specifications: 
Deterministic - Spec define single possible output for given input, or allow implementor to choose from a set of legal outputs?
Declarative - Spec characterize output should be, or explicitly compute  output?
Strong - how large the set of legal implementations the spec has
 

Good Specifications: 
•	Coherent
o	NO lots of different cases/long argument lists/deeply nested if-statements/boolean flags 
•	Informative results
•	Not too strong or too weak 
•	Use abstract types abstract types where possible
 
 
Access control (Public/Private)
Public methods are freely accessible to other parts of the program.  helper methods, internal things private.
Protecting persistent internal state keeps program safe from bugs
 
Static methods: not associated with any particular instance of a class
Instance methods: must be called on a particular object or instance.
•	Specifications for instance methods: same, but will refer to properties of instance (object) on which they were called.

13
[11] Mutability
Mutable objects "representing state", if applied methods, can change its state. Mutable objects to model finite state machines, but difficult to reason program correctness.
Mutation occurs when a value (or object) that a reference variable points to changes.
 
Immutable types can:
•	reduce bugs
•	make code more comprehensible
•	ease code evolution
Multiple places in your program rely on object to remain consistent
 
 
Defensive copying: return a copy of a value which can be freely altered. 
•	However, less space efficient. 
•	Immutable don't need defensively copied
 
Aliases: multiple reference for the same mutable object. Think: instance diagrams.
 
 
Include mutation in method's spec!!
 
Iterators: for loops. Has 2 methods: 
•	next()  returns next element. This is a mutator method (it advances the iterator)
•	hasNext() checks if there is next element
Iterators are effective design patterns (a well-tested solution to a
common design problem
 
Instance variables: aka fields in Java. Consists of:
•	Access modifiers (public private)
•	Types (int, boolean etc.)
•	Variable names
Constructor: makes new object instance, initializes its instance variables.
 
'this' keyword: refer to the instance object. (this.list)
•	To disambiguate two different variables named list (an instance variable and a
constructor parameter) 
 
Mutation undermines Iterator: 
•	If try to change value at index while at index = ConcurrentModificationException
 
Mutable objects reduce changeability
•	make contracts between clients and implementers more complicated
•	reduce freedom of the client and implementer to change
 
Commonly-used immutable types in the Java API:
•	Primitive types and primitive wrappers 
•	Types from java.time. Don't use Date Object
 
Mutable: Java's collections types --- List , Set , Map ---  (ArrayList , HashMap , etc.)
 
The Collections utility class has methods for obtaining unmodifiable views (wrapper around the underlying list/set/map) of these mutable collections:
•	Collections.unmodifiableList
•	Collections.unmodifiableSet
•	Collections.unmodifiableMap
•	Collections.emptyList <- immutable empty collections
 
If have reference to, perform mutations on wrapper, will trigger an UnsupportedOperationException .
 
Before pass mutable collection to another part of our program, wrap in unmodifiable wrapper. Also eliminate reference to the mutable collection to prevent mutation. 
 
Mutable collection inside an unmodifiable wrapper can still be modified, defeating the
wrapper.

ADTs: separate usage of data structure from particular form of the data structure itself
•	dangerous problem: clients' assumptions about the type's internal representation.
•	a type is characterized by the operations you can perform on it. Can be immutable, mutable
o	For ADT, only operations matters
 
Abstraction: Omitting or hiding low-level details.
 
Modularity: Dividing a system into components or modules
•	each can be designed, implemented, tested, reasoned about, and reused separately from the rest of the system.
 
Encapsulation: Building walls around a module (a hard shell or capsule) 
•	So module is responsible for its own internal behavior
•	bugs in other parts of the system cannot damage its integrity.
 
Information hiding: Hiding details of a module's implementation from the rest of the system, so that those details can be changed later without changing the rest of the system.
 
Separation of concerns: Making a feature (or "concern") the responsibility of a single module, rather than spreading it across multiple modules.
 
Operations of an abstract type:
Creators: create new objects of the type. A creator may take an object as an argument, but not an object of the type being constructed. 
•	Constructor methods are creators 
 
Producers create new objects from old objects of the type. 
•	concat() method of String (takes two strings and produces a new one representing their concatenation.)
 
Observers: take objects of the abstract type and return objects of a different type. 
•	size() method of List (returns an int)
 
Mutators change objects. 
•	add() method of List (mutates a list by adding an element to the end)
 
Interface: list of method signatures, no method body. language mechanism for expressing an abstract data type. 
•	other classes provide the actual implementation of the data type
•	specifies the contract for the client and nothing more.
•	With interface, multiple representations of ADT can co-exist in the same program
o	Otherwise, only 1 representation
•	In java, interface not allowed constructors, but allowed static method
o	Factory method: static method as a creator instead of a
Constructor
 
Why Interface?
•	Documentation (for compiler and human) help the compiler catch ADT implementation bugs
•	Performance trade-offs. provide methods with very different performance characteristics. 
•	Flexibility. Different invariant options
•	Optional methods. Can make mutability optional
•	Methods with undetermined specs: 
Implementation 1: slower method implementations, but representation sorted order, allowing quick conversion to a sorted list.
Implementation 2: methods faster by not supporting conversion to sorted lists
•	Multiple views of one class: no need ADT multiple times for different data structure (want to view as widget or a list?)
•	More/less trustworthy: "choose" implementations for applications based on how serious bugs are
 
better to have simple operations that can be combined in powerful ways, rather than lots of complex operations
4
Invariants:  a property of a program that is always true, for every possible runtime state
•	abstract data type preserves its own invariants, meaning
o	creators and producers must establish the invariant for new object instances
o	mutators and observers must preserve the invariant
Structural induction . If an invariant of an abstract data type is
1. established by creators and producers;
2. preserved by mutators, and observers; and
3. no representation exposure occurs,
then the invariant is true of all instances of the abstract data type.
 
Representation exposure: code outside the class can modify the representation directly
•	Beware of mutability of argument types and return types of all ADT operations
 
Types may be:
•	Generic: a list or a set, or a graph OR
•	Domain specific: a street map, an employee database, a phone book, etc.
o	should not mix generic and domain-specific features. 
 
ADTs should be: 
•	Representation independent. 
o	operations offered by List are independent of whether the list is
represented as a linked list or as an array.
o	changes in representation have no effect on code outside the abstract type itself