
# The Art of Readable Code
> Authors: Dustin Boswell and Trevor Foucher

*"We created this book by analyzing hundreds of code examples from production code to figure out what works in practice. We’ve also read many books and articles."*


## Chapter 1. Code Should Be Easy to Understand
-	Code should be: 
	- Written to minimize the time
	- Someone else to understand it
		
-	Is Smaller Always Better? ー＞ No

-	Coworker like it

## Chapter 2. Packing Information into Names
-	Use specific word: 
	- GetPage(url) ー＞ FetchPage(url) or DownloadPage(url).
	- class Thread { void Stop(); ... }: 
		- Stop() ー＞ Kill(), Pause(), Resume()

-	Avoid Generic Names Like tmp, result, retval(return variable):
	- Pick a name that describes the entity’s value or purpose

-	Nested for loops: categories, articles, users:
	- Index values: 
		- i, j, k ー＞ ci, ai, ui　ー＞ debug ez
	- Ex:
		- If (categories[ci]. articles[ui] == users[ai]) #Bug! First letters don't match .
		- If (categories[ci]. articles[ai] == users[ui]) #OK. First letters match.

-	Index in loop: 
	- Interactors loop 		ー＞ i
	- Reverser interactor loop 	ー＞ ri || rit

-	Prefer Concrete Names over Abstract Names
	- ServerCanStart() ー＞ CanListionOnPort()

-	Values with Units: Start Time
	- start ー＞ start_ms

-	Encoding Other Important Attributes: 
	- Just use in where a bug can easily sneak
	- comment ー＞ unescaped_comment

-	Shorter Names Are Okay for Shorter Scope:
	- Ex: Str, char, tmp

-	Acronyms and Abbreviations:
	- If new teammate can understand what the name means
	- BackEndManager ー＞ BEManager

-	Throwing Out Unneeded Words
	- ConvertToString() ー＞ ToString()
	- DoServeLoop() ー＞ ServeLoop()

-	Use Name Formatting to Convey Meaning:

|||
|----------------|----------|
|Class|PascalCase|
|Func, Method|camelCase|
|Var|snake_case|
|Class member var|snake_case_|
|Const|ALL_CAPS|
|JQuery Object|$image|
|Pure CSS|kebab-case|



Note: Use camelCase for declare a CONST in C++, because ALL_CAPS is other default method.

## Chapter 3: Names That Can’t Be Misconstrued
### Asking yourself, “What other meanings could someone interpret from this name?”

-	Example: 
	- Filter() ー＞ Select() or Exclude()
	- Clip(text, length) ー＞ Truncate(text, length)
	- Max_length ー＞ max_chars

-	Inclusive Limits: max_ & min
	- CART_TOO_BIG_LIMIT = 10  ー＞ MAX_ITEMS_IN_CART 

-	Inclusive Ranges: first & last
  
-	Exclusive Ranges: begin & end
	 

-	Naming Booleans
	- Adding words like: is, has, can, should
		- read_password ー＞ need_password ー＞ user_is_authenticated
	- Avoid negated terms in a name: 
		- disable_ssl = false ー＞ use_ssl = true

-	When you want to use other object and linked it
	- If use attribute named like below, someone could misinterpret it:
	- Template: 100
		- I am a template
		-	I am using this other template
	-	Reuse: 100
		- This can be reused at most 100 times
	-	Copy: 100
	- Inherit: 100
		-	This is the 100th copy of something.
		- Copy this 100 times
 

##	Chapter 4: Aesthetics
###  Consistent style is more important than the “right” style.

-	Three Principles: 
	- Use consistent layout. 
	- Make similar code look similar.
	- Group related lines of code into blocks.

-	Line break: 80ー＞100 char

-	Use Column Alignment When Helpful
	- But it takes more work, larger diff being commited when making changes

-	Field declarations order: 
	 - Match with order of fields on the corresponding HTML form
	- Most ー＞ lease important
	- Alphabetically

-	Organize Declarations into Blocks, Paragraphs
	- Use empty lines to break apart large blocks into logical “paragraphs.”
         

##  Chapter 5. Know What to Comment
### The purpose of commenting is to help the reader know as much as the writer did.
### The bester code with comment itself.	

-	Comment :
	- Read comment take time away read code, bester with “new information”
	- Don’t comment on facts that can be quickly from the code itself
 	- Don’t Comment Bad Names—Fix the Names Instead

-	High-level comments:
	> // This file contains helper func for …
-	Include “Director Commentary”: tell stories what code was made
	> // Surprisingly, a binary tree was 40% faster than a hash table for this data.
-	Summary comments
	> // Comment on the “bigger picture”
-	Comment the Flaws in Your Code
	> // TODO(dustin): handle other image formats besides JPEG
 
-	Comment on Your Constants
	- NUM_THREADS = 8 // = 2*num_processors, that's good enough.

##	Chapter 6: Making Comments Precise and Compact
### Comments should have a high information-to-space ratio.

-	Keep Comments Compact
-	Avoid Ambiguous Pronouns
-	Polish Sloppy Sentences
-	Describe Function Behavior Precisely
-	Use Input/Output Examples That Illustrate Corner Cases
-	Intent of Your Code
-	“Named Function Parameter” Comments (default in python)


## Chapter 7. Making Control Flow Easy to Read
### Make all your control flow as “natural”,
### Doesn’t make the reader stop and reread your code.

- The Order of Arguments in Conditionals
	- Do:   	if (length >= 10)
	- Not:  	if (10 <= length)
	
	- Do: 	if (NULL = obj) ー＞ catch bug 
	- Not: 	if (obj = NULL) ー＞ no catch

-	If else with the positive case first

-	Minimizing the number of lines 
	- A better is minimize the time for someone to understand it

-	Avoid While do loop

-	Minimize Nesting
	- Removing Nesting by Returning Early
	- Removing Nesting Inside Loops


## 	Chapter 8. Breaking Down Giant Expressions
### Break more digestible pieces

-	Explaining Variables, Summary Variables:
	 - Named for expression result
 

-	Using De Morgan’s Laws
	- 	Break nest condition ー＞ only not, and, or


##	Chapter 9. Variables and Readability

-	Useless Temporary Variables
	- now = Date.now()
	- User.last_login = now

	-> User.last_login = Date.now()

-	Eliminating Control Flow Variables
	- Boolean done_loop = false
	-> Break in loop, return early

-	Shrink the Scope of Your Variables
	- Make your variable visible by as few lines of code as possible.
	- Moving Definitions Down
		- Definition right before its first use.

-	No Nested Scope in Python and JavaScript
	- Declaration in JavaScript:
		- Do:  &nbsp;&nbsp;&nbsp;&nbsp;	LET & CONST
		- Don’t: &nbsp;	VAR


## Chapter 10. Extracting Unrelated Subproblems
### Separate the generic code to specific code
### Don’t Repeat your self

-	Consider when separate：
	- The high level goal
	- Solving unrelated subproblem
	- Enough lines are solving

-	Pure Utility Code
		- Return a new data, not modifier origin data(parameter)
		- Like a new assign object

-	Simplifying an Existing Interface
		- Create wrapper function to hide the ugly details

##	 Chapter 11. One Task at a Time
###  Code should be organized: One task at a time
- It can be more lines but:
	- 100 lines is easy to read is better than 50 lines?

##	 Chapter 12. Turning Thoughts into Code
-	Code like a plain English
		- Is_owner = (document.artist._id == auth_user._id)

-	Describing program in plain English
		- Using that desc to write natural code


##	 Chapter 13. Writing Less Code
### The most readable code is no code at all.

-	Don’t Bother Implementing That Feature
	- Programmers tend to:
		- Overestimate how many features are truly essential
		- Underestimate how much effort it takes to implement

-	Rethinking to solve the easiest version of the problem


## Chapter 14. Testing and Readability
### Test code should be readable,
### Coworker are comfortable changing or adding tests.

-	Creating the minimal test statement ー＞ Unit test
-	Making Error Messages Readable, easy to track down and fix.
-	Simplifying the Input Values
-	Naming Test Function:
	```
		    FunctionName()
	ー＞ Test_FunctionName()
	ー＞ Test_FunctionName()_Situation()
	```
	 Ex: 	
	```
			SortAndFilterDocs()
	ー＞ Test_SortAndFilterDocs()
	ー＞ Test_SortAndFilterDocs_BasicSorting()
	```


##	 Chapter 15. Designing and Implementing a “Minute/Hour Counter”

The problem: 
> Counter tracking transfer data in past Minute & Hour	

Which design is the best: 
- Native solution
- Conveyor belt design
- Time-bucketed design

Recommend: Read 3 solutions and optimize code design of this problem in the origin book.


----------------
日本語で概要：
https://qiita.com/AKB428/items/20e81ccc8d9998b5535d

Origin book: 
https://www.amazon.co.jp/Art-Readable-Code-Practical-Techniques/dp/0596802293

Other Book on Writing High-Quality Code
- *Code Complete: A Practical Handbook of Software Construction, 2nd edition, by Steve McConnell (Microsoft Press, 2004)*
