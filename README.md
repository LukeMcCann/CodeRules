Power of 10: 

1. Keep Simple Control Flow

    Simple control flows are easier to debug, 
    have cleaner documentation and diagrams, 
    and are generally less prone to bugs. 

    Simple control flow constructs exclude:
	- goto statements
	- setjmp statements
	- longjmp statements
	- recursion

    each of these functions obfuscate the flow
    of the code, recursion especially leads to
    cyclic logic which can be difficult to follow.

    Recursive code can lead to runaway code which
    can cause a crash, especially in embedded systems.


2. Limit all loops

    By giving all loops an explicit (fixed) upper bound
    we avoid all edge cases which may lead to runaway code:

	int list_search (list_t *e, int search) {
           int i = 0; 
           while (e && i++ < MAX_ITER) {
             if (e->value == search) {
		return e;
		e = e->fd;
             }
           }
           return null;
        }
   

   By binding all loops to a hard upper limit we ensure that
   the loop is statically provable. If a tool is unable to 
   prove the loop statically this rule is violated.


3. Don't use the heap

   This isn't possible in all languages.
   By relying entirely on stack memory we reduce
   issues caused by memory leaks, heap overflows,
   and other common issues.


4. Limit Function Size

    A function should do one thing. 
    By ensuring our functions perform
    one and only one actions we cut down
    the amount of code in a given function 
    making it easier to read and understand.


5. Practice Data Hiding

   Data hiding is the practice of declaring
   variables at the lowest scope possible. 
   Data hiding restricts the data access to
   class members to maintain integrity.


6. Check Return Values

   Check all return values for non-void return values.
   This means we should explicitly cast all return values
   to void as to show the return value of a given function
   was intentionally ignored.


7. Limit the Preprocessor

   The preprocessor is a powerful obfuscation tool
   that can destroy code clarity and confuse text-based
   checkers.

   Having flags that can change your code at compile time 
   we essentially create 2^n (n being the number of preprocessor flags)
   build targets that need to be tested, making the code harder to test and maintain.

8. Restrict Pointers Use

   Pointers should not be able to be 
   dereferenced more than one layer at 
   a time. Pointers are a tool that are powerful
   but easy to misuse. We should create structures
   that properly track your pointers.

   This also means to avoid function pointers altogether
   as they obfuscate the code. 

9. Be pendantic 
   
   
