# 🤖 C
Tags: #🤖
Related to: 
See also: 
Previous: [[PROGRAMMING]]

---
# The C Programming Language + The C Answer Book

## 1. A Tutorial Introduction

### Examples

#### Getting Started

##### Print hello, world
```c
#include <stdio.h>

int
main()
{
    printf("hello, world\n");
}
```

##### Try invalid escape sequences
```c
#include <stdio.h>

int
main(void)
{
    printf("hello, world\y");
    printf("hello, world\7");
    printf("hello, world\?");
}
```

##### Print Fahrenheit to Celsius scale
```c
#include <stdio.h>

#define LOWER   0   /* lower limit of table */
#define UPPER   300 /* upper limit */
#define STEP    20  /* step size */

/* print Fahrenheit-Celsius table */
int
main(void)
{
    int fahr;

    for (fahr = LOWER; fahr <= UPPER; fahr += STEP)
        printf("%3d %6.1f\n", fahr, (5.0/9.0)*(fahr-32));
}
```

##### Print Celsius to Fahrenheit scale
```c
#include <stdio.h>

#define LOWER   0   /* lower limit of table */
#define UPPER   300 /* upper limit */
#define STEP    20  /* step size */

/* print Celsius-Fahrenheit table; floating-point version */
int
main(void)
{
    float celsius;

    for (celsius = LOWER; celsius <= UPPER; celsius += STEP)
        printf("%4.0f  %8.1f\n", celsius, (9.0 * celsius) / 5.0 + 32.0);
}
```

##### Print Celsius to Fahrenheit scale in reverse order
```c
#include <stdio.h>

#define LOWER   0   /* lower limit of table */
#define UPPER   300 /* upper limit */
#define STEP    20  /* step size */

/* print Fahrenheit-Celsius table in reverse order*/
int
main(void)
{
    int fahr;

    for (fahr = UPPER; fahr >= LOWER; fahr -= STEP)
        printf("%3d %6.1f\n", fahr, (5.0/9.0)*(fahr-32));
}
```

##### Copy input to output
```c
#include <stdio.h>

int
main(void)
{
    int c;

    while ((c = getchar()) != EOF)
        putchar(c);
}
```

##### Test precedence
```c
#include <stdio.h>

int
main(void)
{
    int c;

    while (c = getchar() != EOF)
        printf("%d\n", c);
    printf("%d - at EOF\n", c);
}
```

##### Print EOF
```c
#include <stdio.h>

int
main(void)
{
    printf("EOF is %d\n", EOF);
}
```

##### Count characters
```c
#include <stdio.h>

/* count characters in input */
int
main(void)
{
    double nc;

    for (nc = 0; getchar() != EOF; ++nc)
        ;
    printf("%.0f\n", nc);
}
```

##### Count lines
```c
#include <stdio.h>

/* count lines in input */
int
main(void)
{
    int c, nl;

    nl = 0;
    while ((c = getchar()) != EOF)
        if (c == '\n')
            ++nl;
    printf("%d\n", nl);
}
```

##### Count blanks, tabs, and newlines
```c
#include <stdio.h>

/* count blanks, tabs, and newlines */
int
main(void)
{
    int c, nb, nt, nl;

    nb = 0; /* number of blanks */
    nt = 0; /* number of tabs */
    nl = 0; /* number of newlines */
    while ((c = getchar()) != EOF)
        if (c == ' ')
            ++nb;
        else if (c == '\t')
            ++nt;
        else if (c == '\n')
            ++nl;
    printf("%d %d %d\n", nb, nt, nl);
}
```

##### Replace blanks
```c
#include <stdio.h>

#define NONBLANK 'A'

/* replace string of blanks with a single blank */
int
main(void)
{
    int c, lastc;

    lastc = NONBLANK;
    while ((c = getchar()) != EOF) {
        if (c != ' ')
            putchar(c);
        else if (c == ' ')
            if (lastc != ' ')
                putchar(c);
        lastc = c;
    }
}
```

##### Replace tab, backspace, and backslash
```c
#include <stdio.h>

/* replace tab, backspace, and backslash with visible characters */
int
main(void)
{
    int c;

    while ((c = getchar()) != EOF)
        if(c == '\t')
            printf("\\t");
        else if (c == '\b')
            printf("\\b");
        else if (c == '\\')
            printf("\\\\");
        else
            putchar(c);
}
```

##### Count characters, words, and newlines
```c
#include <stdio.h>

#define IN  1
#define OUT 0

/* count characters, words, and newlines */
int
main(void)
{
    int c, nc, nw, nl, state;

    nc = nw = nl = 0;
    state = OUT;
    while ((c = getchar()) != EOF) {
        ++nc;
        if (c == '\n')
            ++nl;
        if (c == ' ' || c == '\n' || c == '\t')
            state = OUT;
        else if (state == OUT) {
            state = IN;
            ++nw;
        }
    }
    printf("chars: %d words: %d newlines: %d\n", nc, nw, nl);
}
```

##### Print input one word per line
```c
#include <stdio.h>

#define IN  1
#define OUT 0

/* print input one word per line */
int
main(void)
{
    int c, state;

    state = OUT;
    while ((c = getchar()) != EOF) {
        if (c == ' ' || c == '\n' || c == '\t') {
            if (state == IN) {
                putchar('\n');      /* finish the word */
                state = OUT;           
            }
        } else if (state == OUT) {
                state = IN;         /* beginning of word */
                putchar(c);
        } else                      /* inside a word */
            putchar(c);
    }
}
```

#### Arrays

##### Count digits, whitespace, others
```c
#include <stdio.h>

/* count digits, white space, others */
int
main(void)
{
    int c, i, nwhite, nother;
    int ndigit[10];

    nwhite = nother = 0;
    for (i = 0; i < 10; ++i)
        ndigit[i] = 0;

    while ((c = getchar()) != EOF)
        if (c >= '0' && c <= '9')
            ++ndigit[c-'0'];
        else if (c == ' ' || c == '\n' || c == '\t')
            ++nwhite;
        else
            ++nother;

    printf("digits =");
    for (i = 0; i < 10; ++i)
        printf(" %d", ndigit[i]);
    printf(", white space = %d, other = %d\n", nwhite, nother);
}
```

```c
if (c >= '0' && c <= '9')
	++ndigit[c-'0'];
```

|Dec|Char|
|:----|:----|
|48|0|
|49|1|
|50|2|
|51|3|
|52|4|
|53|5|
|54|6|
|55|7|
|56|8|
|57|9|

##### Print horizontal histogram
```c

```

##### Stub
```c

```

##### Stub
```c

```

##### Stub
```c

```

##### Stub
```c

```

##### Stub
```c

```

### Tables

#### Data types
|Data types|Description|
|:----|:----|
|char|character - a single byte|
|short|short integer|
|long|long integer|
|double|double-precision floating point|

#### Conversion specifications
|Conversion|Description|
|:----|:----|
|%d|print as decimal integer|
|%6d|print as decimal integer, at least 6 characters wide|
|%f|print as floating point|
|%6f|print as floating point, at least 6 characters wide|
|%.2f|print as floating point, 2 characters after decimal point|
|%6.2f|print as floating point, at least 6 wide and 2 after decimal point|
|%o|octal|
|%x|hexadecimal|
|%s|character string|
|% %|for itself|

## 2. Types, Operators and Expressions


## 3. Control Flow


## 3. Functions and Program Structure


## 5. Pointers and Arrays


## 6. Structures


## 7. Input and Output


## 8. The UNIX System Interface


## Appendix A - Reference Manual


## Appendix B - Standard Library

### 1. Input and Output: <stdio.h>

#### 1. File Operations
```c
FILE *
fopen(const char *filename, const char *mode)
// opens the named file, and returns a stream, or NULL if the attempt fails.

FILE *
freopen(const char *filename, const char *mode, FILE *stream)
// freopen opens the file with the specified mode and associates the stream with it. It
// returns stream, or NULL if an error occurs. freopen is normally used to change the
// files associated with stdin, stdout, or stderr.

int
fflush(FILE *stream)
// On an output stream, fflush causes any buffered but unwritten data to be written; on
// an input stream, the effect is undefined. It returns EOF for a write error, and zero
// otherwise. fflush(NULL) flushes all output streams.

int fclose(FILE *stream)
// fclose flushes any unwritten data for stream, discards any unread buffered input,
// frees any automatically allocated buffer, then closes the stream. It returns EOF if any
// errors occurred, and zero otherwise.

int
remove(const char *filename)
// remove removes the named file, so that a subsequent attempt to open it will fail. It
// returns non-zero if the attempt fails.

int
rename(const char *oldname, const char *newname)
// rename changes the name of a file; it returns non-zero if the attempt fails.

FILE *
tmpfile(void)
// tmpfile creates a temporary file of mode "wb+" that will be automatically removed
// when closed or when the program terminates normally. tmpfile returns a stream, or
// NULL if it could not create the file.

char *
tmpnam(char s[L_tmpnam])
// tmpnam(NULL) creates a string that is not the name of an existing file, and returns a
// pointer to an internal static array. tmpnam(s) stores the string in s as well as returning
// it as the function value; s must have room for at least L_tmpnam characters. tmpnam
// generates a different name each time it is called; at most TMP_MAX different names are
// guaranteed during execution of the program. Note that tmpnam creates a name, not a
// file.

int
setvbuf(FILE *stream, char *buf, int mode, size_t size)
// setvbuf controls buffering for the stream; it must be called before reading, writing or
// any other operation. A mode of _IOFBF causes full buffering, _IOLBF line buffering of
// text files, and _IONBF no buffering. If buf is not NULL , it will be used as the buffer,
// otherwise a buffer will be allocated. size determines the buffer size. setvbuf returns
// non-zero for any error.

void
setbuf(FILE *stream, char *buf)
// If buf is NULL, buffering is turned off for the stream. Otherwise, setbuf is equivalent
// to (void) setvbuf(stream, buf, _IOFBF, BUFSIZ).
```

#### 2. Formatted Output
```c
int
fprintf(FILE *stream, const char *format, ...)
// fprintf converts and writes output to stream under the control of format. The return value
// is the number of characters written, or negative if an error occurred.

int
printf(const char *format, ...)
// printf(...) is equivalent to fprintf(stdout, ...).

int
sprintf(char *s, const char *format, ...)
// sprintf is the same as printf except that the output is written into the string s,
// terminated with '\0'. s must be big enough to hold the result. The return count does
// not include the '\0'.

int
vprintf(const char *format, va_list arg)

int
vfprintf(FILE *stream, const char *format, va_list arg)

int
vsprintf(char *s, const char *format, va_list arg)
// The functions vprintf, vfprintf, and vsprintf are equivalent to the corresponding
// printf functions, except that the variable argument list is replaced by arg, which has
// been initialized by the va_start macro and perhaps va_arg calls. See the discussion
// of <stdarg.h> in Section B.7.
```

#### 3. Formatted Input
```c
int
scanf(const char *format, ...)
// The scanf function deals with formatted input conversion.
// scanf(...) is identical to fscanf(stdin, ...).

int
fscanf(FILE *stream, const char *format, ...)
// fscanf reads from stream under control of format , and assigns converted values through
// subsequent arguments, each of which must be a pointer . It returns when format is exhausted.
// fscanf returns EOF if end of file or an error occurs before any conversion; otherwise it returns
// the number of input items converted and assigned.
```

#### 4. Character Input and Output Functions
```c
int
fgetc(FILE *stream)
// fgetc returns the next character of stream as an unsigned char (converted to an
// int), or EOF if end of file or error occurs.

char *
fgets(char *s, int n, FILE *stream)
//  fgets reads at most the next n-1 characters into the array s, stopping if a newline is
// encountered; the newline is included in the array, which is terminated by '\0'. fgets
// returns s, or NULL if end of file or error occurs.

int
fputc(int c, FILE *stream)
// fputc writes the character c (converted to an unsigend char ) on stream. It returns
// the character written, or EOF for error.

int
fputs(const char *s, FILE *stream)
// fputs writes the string s (which need not contain \n) on stream; it returns non-
// negative, or EOF for an error.

int
getc(FILE *stream)
// getc is equivalent to fgetc except that if it is a macro, it may evaluate stream more
// than once.

int
getchar(void)
// getchar is equivalent to getc(stdin).

char *
gets(char *s)
// gets reads the next input line into the array s; it replaces the terminating newline with
// '\0' . It returns s, or NULL if end of file or error occurs.

int
putc(int c, FILE *stream)
// putc is equivalent to fputc except that if it is a macro, it may evaluate stream more
// than once.

int
putchar(int c)
// putchar(c) is equivalent to putc(c,stdout).

int
puts(const char *s)
// puts writes the string s and a newline to stdout. It returns EOF if an error occurs,
// non-negative otherwise.

int
ungetc(int c, FILE *stream)
// ungetc pushes c (converted to an unsigned char) back onto stream, where it will be
// returned on the next read. Only one character of pushback per stream is guaranteed.
// EOF may not be pushed back. ungetc returns the character pushed back, or EOF for
// error.
```

#### 5. Direct Input and Output Functions
```c
size_t
fread(void *ptr, size_t size, size_t nobj, FILE *stream)
// fread reads from stream into the array ptr at most nobj objects of size size . fread
// returns the number of objects read; this may be less than the number requested. feof
// and ferror must be used to determine status.

size_t
fwrite(const void *ptr, size_t size, size_t nobj, FILE *stream)
// fwrite writes, from the array ptr, nobj objects of size size on stream. It returns the
// number of objects written, which is less than nobj on error.
```

#### 6. File Positioning Functions
```c
int
fseek(FILE *stream, long offset, int origin)
// fseek sets the file position for stream; a subsequent read or write will access data
// beginning at the new position. For a binary file, the position is set to offset
// characters from origin, which may be SEEK_SET (beginning), SEEK_CUR (current
// position), or SEEK_END (end of file). For a text stream, offset must be zero, or a value
// returned by ftell (in which case origin must be SEEK_SET ). fseek returns non-zero
// on error.

long
ftell(FILE *stream)
// ftell returns the current file position for stream, or -1 on error.

void
rewind(FILE *stream)
// rewind(fp) is equivalent to fseek(fp, 0L, SEEK_SET); clearerr(fp).

int
fgetpos(FILE *stream, fpos_t *ptr)
// fgetpos records the current position in stream in *ptr, for subsequent use by
// fsetpos. The type fpos_t is suitable for recording such values. fgetpos returns non-
// zero on error.

int
fsetpos(FILE *stream, const fpos_t *ptr)
// fsetpos positions stream at the position recorded by fgetpos in *ptr. fsetpos
// returns non-zero on error.
```

#### 7. Error Functions
```c
void
clearerr(FILE *stream)
// clearerr clears the end of file and error indicators for stream.

int
feof(FILE *stream)
// feof returns non-zero if the end of file indicator for stream is set.

int
ferror(FILE *stream)
// ferror returns non-zero if the error indicator for stream is set.

void
perror(const char *s)
// perror(s) prints s and an implementation-defined error message corresponding to
// the integer in errno, as if by fprintf(stderr, "%s: %s\n", s, " error message ");
```

### 2. Character Class Tests: <ctype.h>
```
isalnum(c)		isalpha(c) or isdigit(c) is true
isalpha(c)		isupper(c) or islower(c) is true
iscntrl(c)		control character
isdigit(c)		decimal digit
isgraph(c)		printing character except space
islower(c)		lower-case letter
isprint(c)		printing character including space
ispunct(c)		printing character except space or letter or digit
isspace(c)		space, formfeed, newline, carriage return, tab, vertical tab
isupper(c)		upper-case letter
isxdigit(c)		hexadecimal digit

int tolower(c)	convert c to lower case
int toupper(c)	convert c to upper case
```

### 3. String Functions: <string.h>
```c
char *
strcpy(s,ct)
// copy string ct to string s, including '\0'; return s.

char
*strncpy(s,ct,n)
// copy at most n characters of string ct to s; return s. Pad with '\0' 's
// if ct has fewer than n characters.

char *
strcat(s,ct)
// concatenate string ct to end of string s; return s.

char *
strncat(s,ct,n)
// concatenate at most n characters of string ct to string s, terminate s
// with '\0'; return s.

int
strcmp(cs,ct)
// compare string cs to string ct, return <0 if cs<ct, 0 if cs==ct, or >0
// if cs>ct.

int
strncmp(cs,ct,n)
// compare at most n characters of string cs to string ct; return <0 if
// cs<ct, 0 if cs==ct, or >0 if cs>ct.

char *
strchr(cs,c)
// return pointer to first occurrence of c in cs or NULL if not present.

char *
strrchr(cs,c)
// return pointer to last occurrence of c in cs or NULL if not present.

size_t
strspn(cs,ct)
// return length of prefix of cs consisting of characters in ct.

size_t
strcspn(cs,ct)
// return length of prefix of cs consisting of characters not in ct.

char
*strpbrk(cs,ct)
// return pointer to first occurrence in string cs of any character string
// ct, or NULL if not present.

char *
strstr(cs,ct)
// return pointer to first occurrence of string ct in cs, or NULL if not
// present.

size_t
strlen(cs)
// return length of cs.

char *
strerror(n)
// return pointer to implementation-defined string corresponding to
// error n.

char *
strtok(s,ct)
// strtok searches s for tokens delimited by characters from ct;

void
*memcpy(s,ct,n)
// copy n characters from ct to s, and return s.

void
*memmove(s,ct,n)
// same as memcpy except that it works even if the objects overlap.

int
memcmp(cs,ct,n)
// compare the first n characters of cs with ct; return as with strcmp.

void
*memchr(cs,c,n)
// return pointer to first occurrence of character c in cs, or NULL if not
// present among the first n characters.

void *memset(s,c,n)
// place character c into first n characters of s, return s.
```

### 4. Mathematical Functions: <math.h>
```
sin(x)				sine of x
cos(x)				cosine of x
tan(x)				tangent of x
asin(x)				sin -1 (x) in range [-pi/2,pi/2], x in [-1,1].
acos(x)				cos -1 (x) in range [0,pi], x in [-1,1].
atan(x)				tan -1 (x) in range [-pi/2,pi/2].
atan2(y,x)			tan -1 (y/x) in range [-pi,pi].
sinh(x)				hyperbolic sine of x
cosh(x)				hyperbolic cosine of x
tanh(x)				hyperbolic tangent of x
exp(x)				exponential function e x
log(x)				natural logarithm ln(x), x >0.
log10(x)			base 10 logarithm log 10 (x), x >0.
pow(x,y)			x y. A domain error occurs if x=0 and y<=0 , or if x<0 and y is not an integer.
sqrt(x)				sqare root of x, x>=0.
ceil(x)				smallest integer not less than x , as a double.
floor(x)			largest integer not greater than x , as a double.
fabs(x)				absolute value |x|
ldexp(x,n)			x*2 n

frexp(x, int *ip)	splits x into a normalized fraction in the interval [1/2,1) which is returned,
					and a power of 2, which is stored in *exp. If x is zero, both parts of the
					result are zero.

modf(x, double *ip)	splits x into integral and fractional parts, each with the same sign as x. It
					stores the integral part in *ip, and returns the fractional part.

fmod(x,y)			floating-point remainder of x/y, with the same sign as x. If y is zero, the
					result is implementation-defined.
```

### 5. Utility Functions: <stdlib.h>
```c
double
atof(const char *s)
// atof converts s to double; it is equivalent to strtod(s, (char**)NULL).

int
atoi(const char *s)
// converts s to int; it is equivalent to (int)strtol(s, (char**)NULL, 10).

long
atol(const char *s)
// converts s to long; it is equivalent to strtol(s, (char**)NULL, 10).

double
strtod(const char *s, char **endp)
// strtod converts the prefix of s to double, ignoring leading white space; it stores a
// pointer to any unconverted suffix in *endp unless endp is NULL. If the answer would
// overflow, HUGE_VAL is returned with the proper sign; if the answer would underflow,
// zero is returned. In either case errno is set to ERANGE.

long
strtol(const char *s, char **endp, int base)
// strtol converts the prefix of s to long, ignoring leading white space; it stores a
// pointer to any unconverted suffix in *endp unless endp is NULL. If base is between 2
// and 36, conversion is done assuming that the input is written in that base. If base is
// zero, the base is 8, 10, or 16; leading 0 implies octal and leading 0x or 0X
// hexadecimal. Letters in either case represent digits from 10 to base-1 ; a leading 0x or
// 0X is permitted in base 16. If the answer would overflow, LONG_MAX or LONG_MIN is
// returned, depending on the sign of the result, and errno is set to ERANGE.

unsigned long
strtoul(const char *s, char **endp, int base)
// strtoul is the same as strtol except that the result is unsigned long and the error
// value is ULONG_MAX.

int
rand(void)
// rand returns a pseudo-random integer in the range 0 to RAND_MAX, which is at least
// 32767.

void
srand(unsigned int seed)
// srand uses seed as the seed for a new sequence of pseudo-random numbers. The
// initial seed is 1.

void *
calloc(size_t nobj, size_t size)
// calloc returns a pointer to space for an array of nobj objects, each of size size, or
// NULL if the request cannot be satisfied. The space is initialized to zero bytes.

void *
malloc(size_t size)
// malloc returns a pointer to space for an object of size size, or NULL if the request
// cannot be satisfied. The space is uninitialized.

void *
realloc(void *p, size_t size)
// realloc changes the size of the object pointed to by p to size. The contents will be
// unchanged up to the minimum of the old and new sizes. If the new size is larger, the
// new space is uninitialized. realloc returns a pointer to the new space, or NULL if the
// request cannot be satisfied, in which case *p is unchanged.

void
free(void *p)
// free deallocates the space pointed to by p; it does nothing if p is NULL. p must be a
// pointer to space previously allocated by calloc, malloc, or realloc.

void
abort(void)
// abort causes the program to terminate abnormally, as if by raise(SIGABRT).

void
exit(int status)
// exit causes normal program termination. atexit functions are called in reverse order
// of registration, open files are flushed, open streams are closed, and control is returned
// to the environment. How status is returned to the environment is implementation-
// dependent, but zero is taken as successful termination. The values EXIT_SUCCESS and
// EXIT_FAILURE may also be used.

int
atexit(void (*fcn)(void))
// atexit registers the function fcn to be called when the program terminates normally;
// it returns non-zero if the registration cannot be made.

int
system(const char *s)
// system passes the string s to the environment for execution. If s is NULL, system
// returns non-zero if there is a command processor. If s is not NULL, the return value is
// implementation-dependent.

char *
getenv(const char *name)
// getenv returns the environment string associated with name, or NULL if no string
// exists. Details are implementation-dependent.

void *
bsearch(const void *key, const void *base, size_t n, size_t size, int (*cmp)(const void *keyval, const void *datum))
// bsearch searches base[0]...base[n-1] for an item that matches *key. The function
// cmp must return negative if its first argument (the search key) is less than its second (a
// table entry), zero if equal, and positive if greater. Items in the array base must be in
// ascending order. bsearch returns a pointer to a matching item, or NULL if none exists.

void
qsort(void *base, size_t n, size_t size, int (*cmp)(const void *, const void *))
// qsort sorts into ascending order an array base[0]...base[n-1] of objects of size
// size. The comparison function cmp is as in bsearch.

int
abs(int n)
// abs returns the absolute value of its int argument.

long
labs(long n)
// labs returns the absolute value of its long argument.

div_t
div(int num, int denom)
// div computes the quotient and remainder of num/denom. The results are stored in the
// int members quot and rem of a structure of type div_t.

ldiv_t
ldiv(long num, long denom)
// ldiv computes the quotient and remainder of num/denom. The results are stored in the
// long members quot and rem of a structure of type ldiv_t.
```

### 6. Diagnostics: <assert.h>

The assert macro is used to add diagnostics to programs:

	void assert(int expression)

If expression is zero when

	assert(expression)

is executed, the assert macro will print on stderr a message, such as

	Assertion failed: expression, file filename, line nnn

It then calls abort to terminate execution. The source filename and line number come from
the preprocessor macros

	__FILE__ and __LINE__

If NDEBUG is defined at the time <assert.h> is included, the assert macro is ignored.

### 7. Variable Argument Lists: <stdarg.h>
The header <stdarg.h> provides facilities for stepping through a list of function arguments
of unknown number and type.

Suppose lastarg is the last named parameter of a function f with a variable number of
arguments. Then declare within f a variable of type va_list that will point to each argument
in turn:

	va_list ap;

ap must be initialized once with the macro va_start before any unnamed argument is
accessed:

	va_start(va_list ap, lastarg);

Thereafter, each execution of the macro va_arg will produce a value that has the type and
value of the next unnamed argument, and will also modify ap so the next use of va_arg
returns the next argument:

	type va_arg(va_list ap, type );

The macro

	void va_end(va_list ap);
	
must be called once after the arguments have been processed but before f is exited.

### 8. Non-local Jumps: <setjmp.h>
```c
int
setjmp(jmp_buf env)
// The macro setjmp saves state information in env for use by longjmp. The return is
// zero from a direct call of setjmp, and non-zero from a subsequent call of longjmp. A
// call to setjmp can only occur in certain contexts, basically the test of if, switch, and
// loops, and only in simple relational expressions.
	
if (setjmp(env) == 0)
	/* get here on direct call */
else
	/* get here by calling longjmp */

void
longjmp(jmp_buf env, int val)
// longjmp restores the state saved by the most recent call to setjmp, using the
// information saved in env, and execution resumes as if the setjmp function had just
// executed and returned the non-zero value val. The function containing the setjmp
// must not have terminated. Accessible objects have the values they had at the time
// longjmp was called, except that non-volatile automatic variables in the function
// calling setjmp become undefined if they were changed after the setjmp call.
```

### 9. Signals: <signal.h>
```c
void
(*signal(int sig, void (*handler)(int)))(int)
// signal determines how subsequent signals will be handled. If handler is SIG_DFL, the
// implementation-defined default behavior is used, if it is SIG_IGN, the signal is ignored;
// otherwise, the function pointed to by handler will be called, with the argument of the type of
// signal. Valid signals include

SIGABRT		abnormal termination	e.g., from abort
SIGFPE		arithmetic error		e.g., zero divide or overflow
SIGILL		illegal function image	e.g., illegal instruction
SIGINT		interactive attention	e.g., interrupt
SIGSEGV		illegal storage access	e.g., access outside memory limits
SIGTERM		termination request sent to this program

// signal returns the previous value of handler for the specific signal, or SIG_ERR if an error
// occurs.

// When a signal sig subsequently occurs, the signal is restored to its default behavior; then the
// signal-handler function is called, as if by (*handler)(sig). If the handler returns, execution
// will resume where it was when the signal occurred.
// The initial state of signals is implementation-defined.

int
raise(int sig)
// raise sends the signal sig to the program; it returns non-zero if unsuccessful.

```

### 10. Date and Time Functions: <time.h>
```c
clock_t and time_t	// arithmetic types representing times

struct tm			// holds the components of a calendar time:
	int tm_sec;		// seconds after the minute (0,61)
	int tm_min;		// minutes after the hour (0,59)
	int tm_hour;	// hours since midnight (0,23)
	int tm_mday;	// day of the month (1,31)
	int tm_mon;		// months since January (0,11)
	int tm_year;	// years since 1900
	int tm_wday;	// days since Sunday (0,6)
	int tm_yday;	// days since January 1 (0,365)
	int tm_isdst;	// Daylight Saving Time flag

// tm_isdst is positive if Daylight Saving Time is in effect, zero if not, and negative if the
// information is not available.

clock_t clock(void)
// clock returns the processor time used by the program since the beginning of
// execution, or -1 if unavailable. clock()/CLK_PER_SEC is a time in seconds.

time_t
time(time_t *tp)
// time returns the current calendar time or -1 if the time is not available. If tp is not
// NULL, the return value is also assigned to *tp.

double
difftime(time_t time2, time_t time1)
// difftime returns time2-time1 expressed in seconds.

time_t
mktime(struct tm *tp)
// mktime converts the local time in the structure *tp into calendar time in the same
// representation used by time. The components will have values in the ranges shown.
// mktime returns the calendar time or -1 if it cannot be represented.

char *
asctime(const struct tm *tp)
// asctime</tt< converts the time in the structure *tp into a string of the form
// Sun Jan 3 15:14:13 1988\n\0

char *
ctime(const time_t *tp)
// ctime converts the calendar time *tp to local time; it is equivalent to
// asctime(localtime(tp))

struct tm *
gmtime(const time_t *tp)
// gmtime converts the calendar time *tp into Coordinated Universal Time
// (UTC). It returns NULL if UTC is not available. The name gmtime has
// historical significance.

struct tm *
localtime(const time_t *tp)
// localtime converts the calendar time *tp into local time.

size_t
strftime(char *s, size_t smax, const char *fmt, const struct tm *tp)
// strftime formats date and time information from *tp into s according
// to fmt, which is analogous to a printf format. Ordinary characters
// (including the terminating '\0') are copied into s. Each %c is
// replaced as described below, using values appropriate for the local
// environment. No more than smax characters are placed into s. strftime
// returns the number of characters, excluding the '\0', or zero if more
// than smax characters were produced.
%a	// abbreviated weekday name.
%A 	// full weekday name.
%b 	// abbreviated month name.
%B 	// full month name.
%c 	// local date and time representation.
%d 	// day of the month ( 01-31 ).
%H 	// hour (24-hour clock) (00-23) .
%I 	// hour (12-hour clock) (01-12) .
%j 	// day of the year (001-366) .
%m 	// month (01-12) .
%M 	// minute (00-59) .
%p 	// local equivalent of AM or PM.
%S 	// second (00-61) .
%U 	// week number of the year (Sunday as 1st day of week) (00-53) .
%w 	// weekday ( 0-6 , Sunday is 0).
%W 	// week number of the year (Monday as 1st day of week) (00-53) .
%x 	// local date representation.
%X 	// local time representation.
%y 	// year without century (00-99) .
%Y 	// year with century.
%Z 	// time zone name, if any.
%% 	// %
```

### 11. Implementation-defined Limits: <limits.h> and <float.h>
The header <limits.h> defines constants for the sizes of integral types.
The values below are acceptable minimum magnitudes; larger values may be
used.
```c
CHAR_BIT 	8 						// bits in a char
CHAR_MAX 	UCHAR_MAX or SCHAR_MAX 	// maximum value of char
CHAR_MIN 	0 or SCHAR_MIN 			// maximum value of char
INT_MAX 	32767 					// maximum value of int
INT_MIN 	-32767 					// minimum value of int
LONG_MAX 	2147483647 				// maximum value of long
LONG_MIN 	-2147483647 			// minimum value of long
SCHAR_MAX 	+127 					// maximum value of signed char
SCHAR_MIN 	-127 					// minimum value of signed char
SHRT_MAX 	+32767 					// maximum value of short
SHRT_MIN 	-32767 					// minimum value of short
UCHAR_MAX 	255 					// maximum value of unsigned char
UINT_MAX 	65535 					// maximum value of unsigned int
ULONG_MAX 	4294967295 				// maximum value of unsigned long
USHRT_MAX 	65535 					// maximum value of unsigned short
```

The names in the table below, a subset of <float.h>, are constants related
to floating-point arithmetic. When a value is given, it represents the
minimum magnitude for the corresponding quantity. Each implementation
defines appropriate values.
```c
FLT_RADIX		2		// radix of exponent, representation, e.g., 2, 16
FLT_ROUNDS				// floating-point rounding mode for addition
FLT_DIG		 	6 		// decimal digits of precision
FLT_EPSILON 	1E-5 	// smallest number x such that 1.0+x != 1.0
FLT_MANT_DIG			// number of base FLT_RADIX in mantissa
FLT_MAX			1E+37	// maximum floating-point number
FLT_MAX_EXP				// maximum n such that FLT_RADIX n-1 is representable
FLT_MIN			1E-37	// minimum normalized floating-point number
FLT_MIN_EXP				// minimum n such that 10 n is a normalized number
DBL_DIG	 		10 		// decimal digits of precision
DBL_EPSILON	 	1E-9 	// smallest number x such that 1.0+x != 1.0
DBL_MANT_DIG			// number of base FLT_RADIX in mantissa
DBL_MAX			1E+37	// maximum double floating-point number
DBL_MAX_EXP				// maximum n such that FLT_RADIX n-1 is representable
DBL_MIN			1E-37	// minimum normalized double floating-point number
DBL_MIN_EXP				// minimum n such that 10 n is a normalized number
```

## Appendix C - Summary of Changes

# The C Puzzle Book

## 1. Operators
## 2. Basic Types
## 3. Control Flow
## 4. Programming Style
## 5. Storage Classes
## 6. Pointers and Arrays
## 7. Structures
## 8. Preprocessor

# Advanced Programming in the Unix Environment

## 1. UNIX System Overview

### Examples

#### List all the files in a directory
```c
#include "apue.h"
#include <dirent.h>

int
main(int argc, char *argv[])
{
	DIR				*dp;
	struct dirent	*dirp;

	if (argc != 2)
		err_quit("usage: ls directory_name");

	if ((dp = opendir(argv[1])) == NULL)
		err_sys("can't open %s", argv[1]);
	while ((dirp = readdir(dp)) != NULL)
		printf("%s\n", dirp->d_name);

	closedir(dp);
	exit(0);
}
```

####  Copy standard input to standard output, using standard I/O
```c
#include "apue.h"

int
main(void)
{
	int		c;

	while ((c = getc(stdin)) != EOF)
		if (putc(c, stdout) == EOF)
			err_sys("output error");

	if (ferror(stdin))
		err_sys("input error");

	exit(0);
}
```

#### Print the process ID
```c
#include "apue.h"

int
main(void)
{
	printf("hello world from process ID %ld\n", (long)getpid());
	exit(0);
}
```

#### Read commands from standard input and execute them
```c
#include "apue.h"
#include <sys/wait.h>

static void	sig_int(int);		/* our signal-catching function */

int
main(void)
{
	char	buf[MAXLINE];	/* from apue.h */
	pid_t	pid;
	int		status;

	if (signal(SIGINT, sig_int) == SIG_ERR)
		err_sys("signal error");

	printf("%% ");	/* print prompt (printf requires %% to print %) */
	while (fgets(buf, MAXLINE, stdin) != NULL) {
		if (buf[strlen(buf) - 1] == '\n')
			buf[strlen(buf) - 1] = 0; /* replace newline with null */

		if ((pid = fork()) < 0) {
			err_sys("fork error");
		} else if (pid == 0) {		/* child */
			execlp(buf, buf, (char *)0);
			err_ret("couldn't execute: %s", buf);
			exit(127);
		}

		/* parent */
		if ((pid = waitpid(pid, &status, 0)) < 0)
			err_sys("waitpid error");
		printf("%% ");
	}
	exit(0);
}

void
sig_int(int signo)
{
	printf("interrupt\n%% ");
}
```

#### Demonstrate strerror and perror
```c
#include "apue.h"
#include <errno.h>

int
main(int argc, char *argv[])
{
	fprintf(stderr, "EACCES: %s\n", strerror(EACCES));
	errno = ENOENT;
	perror(argv[0]);
	exit(0);
}
```

#### Print user ID and group ID
```c
#include "apue.h"

int
main(void)
{
	printf("uid = %d, gid = %d\n", getuid(), getgid());
	exit(0);
}
```

### Tables

#### Common shells used on UNIX systems
|Name|Path|FreeBSD 8.0|Linux 3.2.0|Mac OS X 10.6.8|Solaris 10|
|:----|:----|:----|:----|:----|:----|
|Bourne shell|/bin/sh|•|•|copy of bash|•|
|Bourne-again shell|/bin/bash|optional|•|•|•|
|C shell|/bin/csh|link to tcsh|optional|link to tcsh|•|
|Korn shell|/bin/ksh|optional|optional|•|•|
|TENEX C shell|/bin/tcsh|•|optional|•|•|

## 2. UNIX Standardization and Implementations

### Function Prototypes

#### The runtime limits are obtained by calling one of the following three functions.
```c
#include <unistd.h>

long
sysconf(int name);

long
pathconf(const char *pathname, int name);

long
fpathconf(int fd, int name);

All three return: corresponding value if OK, −1 on error (see later)
```

##### Data size options and name arguments to sysconf
|Name of option	Description	name argument|
|:----|
|_POSIX_V7_ILP32_OFF32	int| long| pointer| and off_t types are 32 bits.	_SC_V7_ILP32_OFF32|
|_POSIX_V7_ILP32_OFFBIG	int| long| and pointer types are 32 bits; off_t types are at least 64 bits.	_SC_V7_ILP32_OFFBIG|
|_POSIX_V7_LP64_OFF64	int types are 32 bits; long| pointer| and off_t types are 64 bits.	_SC_V7_LP64_OFF64|
|_POSIX_V7_LP64_OFFBIG	_POSIX_V7_LP64_OFFBIG int types are at least 32 bits; long| pointer| and off_t types are at least 64 bits.	_SC_V7_LP64_OFFBIG|

### Examples

#### Print all possible sysconf and pathconf values (truncated)
```c
#include "apue.h"
#include <errno.h>
#include <limits.h>

static void pr_sysconf(char *, int);
static void pr_pathconf(char *, char *, int);

int
main(int argc, char *argv[])
{
	if (argc != 2)
		err_quit("usage: a.out <dirname>");

#ifdef ARG_MAX
	printf("ARG_MAX defined to be %ld\n", (long)ARG_MAX+0);
#else
	printf("no symbol for ARG_MAX\n");
#endif
#ifdef _SC_ARG_MAX
	pr_sysconf("ARG_MAX =", _SC_ARG_MAX);
#else
	printf("no symbol for _SC_ARG_MAX\n");
#endif

#ifdef FILESIZEBITS
	printf("FILESIZEBITS defined to be %ld\n", (long)FILESIZEBITS+0);
#else
	printf("no symbol for FILESIZEBITS\n");
#endif
#ifdef _PC_FILESIZEBITS
	pr_pathconf("FILESIZEBITS =", argv[1], _PC_FILESIZEBITS);
#else
	printf("no symbol for _PC_FILESIZEBITS\n");
#endif

	exit(0);
}

static void
pr_sysconf(char *mesg, int name)
{
	long	val;

	fputs(mesg, stdout);
	errno = 0;
	if ((val = sysconf(name)) < 0) {
		if (errno != 0) {
			if (errno == EINVAL)
				fputs(" (not supported)\n", stdout);
			else
				err_sys("sysconf error");
		} else {
			fputs(" (no limit\n)", stdout);
		}
	} else {
		printf(" %ld\n", val);
	}
}

static void
pr_pathconf(char *mesg, char *path, int name)
{
	long	val;

	fputs(mesg, stdout);
	errno = 0;
	if ((val = pathconf(path, name)) < 0) {
		if (errno != 0) {
			if (errno == EINVAL)
				fputs(" (not supported)\n", stdout);
			else
				err_sys("pathconf error, path = %s", path);
		} else {
			fputs(" (no limit)\n", stdout);
		}
	} else {
		printf(" %ld\n", val);
	}
}
```

#### Dynamically allocate space for a pathname
```c
#include "apue.h"
#include <errno.h>
#include <limits.h>

#ifdef	PATH_MAX
static long	pathmax = PATH_MAX;
#else
static long	pathmax = 0;
#endif

static long	posix_version = 0;
static long	xsi_version = 0;

/* If PATH_MAX is indeterminate, no guarantee this is adequate */
#define	PATH_MAX_GUESS	1024

char *
path_alloc(size_t *sizep) /* also return allocated size, if nonnull */
{
	char	*ptr;
	size_t	size;

	if (posix_version == 0)
		posix_version = sysconf(_SC_VERSION);

	if (xsi_version == 0)
		xsi_version = sysconf(_SC_XOPEN_VERSION);

	if (pathmax == 0) {		/* first time through */
		errno = 0;
		if ((pathmax = pathconf("/", _PC_PATH_MAX)) < 0) {
			if (errno == 0)
				pathmax = PATH_MAX_GUESS;	/* it's indeterminate */
			else
				err_sys("pathconf error for _PC_PATH_MAX");
		} else {
			pathmax++;		/* add one since it's relative to root */
		}
	}

	/*
	 * Before POSIX.1-2001, we aren't guaranteed that PATH_MAX includes
	 * the terminating null byte.  Same goes for XPG3.
	 */
	if ((posix_version < 200112L) && (xsi_version < 4))
		size = pathmax + 1;
	else
		size = pathmax;

	if ((ptr = malloc(size)) == NULL)
		err_sys("malloc error for pathname");

	if (sizep != NULL)
		*sizep = size;
	return(ptr);
}
```

#### Determine the number of file descriptors
```c
#include "apue.h"
#include <errno.h>
#include <limits.h>

#ifdef	OPEN_MAX
static long	openmax = OPEN_MAX;
#else
static long	openmax = 0;
#endif

/*
 * If OPEN_MAX is indeterminate, this might be inadequate.
 */
#define	OPEN_MAX_GUESS	256

long
open_max(void)
{
	if (openmax == 0) {		/* first time through */
		errno = 0;
		if ((openmax = sysconf(_SC_OPEN_MAX)) < 0) {
			if (errno == 0)
				openmax = OPEN_MAX_GUESS;	/* it's indeterminate */
			else
				err_sys("sysconf error for _SC_OPEN_MAX");
		}
	}
	return(openmax);
}
```

### Tables

#### Headers defined by the ISO C standard
|Header|FreeBSD 8.0|Linux 3.2.0|Mac OS X 10.6.8|Solaris 10|Description|
|:----|:----|:----|:----|:----|:----|
|<assert.h>|•|•|•|•|verify program assertion|
|<complex.h>|•|•|•|•|complex arithmetic support|
|<ctype.h>|•|•|•|•|character classification and mapping support|
|<errno.h>|•|•|•|•|error codes (Section 1.7)|
|<fenv.h>|•|•|•|•|floating-point environment|
|<float.h>|•|•|•|•|floating-point constants and characteristics|
|<inttypes.h>|•|•|•|•|integer type format conversion|
|<iso646.h>|•|•|•|•|macros for assignment, relational, and unary operators|
|<limits.h>|•|•|•|•|implementation constants (Section 2.5)|
|<locale.h>|•|•|•|•|locale categories and related definitions|
|<math.h>|•|•|•|•|mathematical function and type declarations and constants|
|<setjmp.h>|•|•|•|•|nonlocal goto (Section 7.10)|
|<signal.h>|•|•|•|•|signals (Chapter 10)|
|<stdarg.h>|•|•|•|•|variable argument lists|
|<stdbool.h>|•|•|•|•|Boolean type and values|
|<stddef.h>|•|•|•|•|standard definitions|
|<stdint.h>|•|•|•|•|integer types|
|<stdio.h>|•|•|•|•|standard I/O library (Chapter 5)|
|<stdlib.h>|•|•|•|•|utility functions|
|<string.h>|•|•|•|•|string operations|
|<tgmath.h>|•|•|•|•|type-generic math macros|
|<time.h>|•|•|•|•|time and date (Section 6.10)|
|<wchar.h>|•|•|•|•|extended multibyte and wide character support|
|<wctype.h>|•|•|•|•|wide character classification and mapping support|

#### Required headers defined by the POSIX standard
|Header|FreeBSD 8.0|Linux 3.2.0|Mac OS X 10.6.8|Solaris 10|Description|
|:----|:----|:----|:----|:----|:----|
|<aio.h>|•|•|•|•|asynchronous I/O|
|<cpio.h>|•|•|•|•|cpio archive values|
|<dirent.h>|•|•|•|•|directory entries (Section 4.22)|
|<dlfcn.h>|•|•|•|•|dynamic linking|
|<fcntl.h>|•|•|•|•|file control (Section 3.14)|
|<fnmatch.h>|•|•|•|•|filename-matching types|
|<glob.h>|•|•|•|•|pathname pattern-matching and generation|
|<grp.h>|•|•|•|•|group file (Section 6.4)|
|<iconv.h>|•|•|•|•|codeset conversion utility|
|<langinfo.h>|•|•|•|•|language information constants|
|<monetary.h>|•|•|•|•|monetary types and functions|
|<netdb.h>|•|•|•|•|network database operations|
|<nl_types.h>|•|•|•|•|message catalogs|
|<poll.h>|•|•|•|•|poll function (Section 14.4.2)|
|<pthread.h>|•|•|•|•|threads (Chapters 11 and 12)|
|<pwd.h>|•|•|•|•|password file (Section 6.2)|
|<regex.h>|•|•|•|•|regular expressions|
|<sched.h>|•|•|•|•|execution scheduling|
|<semaphore.h>|•|•|•|•|semaphores|
|<strings.h>|•|•|•|•|string operations|
|<tar.h>|•|•|•|•|tar archive values|
|<termios.h>|•|•|•|•|terminal I/O (Chapter 18)|
|<unistd.h>|•|•|•|•|symbolic constants|
|<wordexp.h>|•|•|•|•|word-expansion definitions|
| | | | | | |
|<arpa/inet.h>|•|•|•|•|Internet definitions (Chapter 16)|
|<net/if.h>|•|•|•|•|socket local interfaces (Chapter 16)|
|<netinet/in.h>|•|•|•|•|Internet address family (Section 16.3)|
|<netinet/tcp.h>|•|•|•|•|Transmission Control Protocol definitions|
| | | | | | |
|<sys/mman.h>|•|•|•|•|memory management declarations|
|<sys/select.h>|•|•|•|•|select function (Section 14.4.1)|
|<sys/socket.h>|•|•|•|•|sockets interface (Chapter 16)|
|<sys/stat.h>|•|•|•|•|file status (Chapter 4)|
|<sys/statvfs.h>|•|•|•|•|file system information|
|<sys/times.h>|•|•|•|•|process times (Section 8.17)|
|<sys/types.h>|•|•|•|•|primitive system data types (Section 2.8)|
|<sys/un.h>|•|•|•|•|UNIX domain socket definitions (Section 17.2)|
|<sys/utsname.h>|•|•|•|•|system name (Section 6.9)|
|<sys/wait.h>|•|•|•|•|process control (Section 8.6)|


#### XSI optional headers defined by the POSIX standard
|Header|FreeBSD 8.0|Linux 3.2.0|Mac OS X 10.6.8|Solaris 10|Description|
|:----|:----|:----|:----|:----|:----|
|<fmtmsg.h>|•|•|•|•|message display structures|
|<ftw.h>|•|•|•|•|file tree walking (Section 4.22)|
|<libgen.h>|•|•|•|•|pathname management functions|
|<ndbm.h>|•| |•|•|database operations|
|<search.h>|•|•|•|•|search tables|
|<syslog.h>|•|•|•|•|system error logging (Section 13.4)|
|<utmpx.h>| |•|•|•|user accounting database|
| | | | | | |
|<sys/ipc.h>|•|•|•|•|IPC (Section 15.6)|
|<sys/msg.h>|•|•|•|•|XSI message queues (Section 15.7)|
|<sys/resource.h>|•|•|•|•|resource operations (Section 7.11)|
|<sys/sem.h>|•|•|•|•|XSI semaphores (Section 15.8)|
|<sys/shm.h>|•|•|•|•|XSI shared memory (Section 15.9)|
|<sys/time.h>|•|•|•|•|time types|
|<sys/uio.h>|•|•|•|•|vector I/O operations (Section 14.6)|

#### Optional headers defined by the POSIX standard
|Header|FreeBSD 8.0|Linux 3.2.0|Mac OS X 10.6.8|Solaris 10|Description|
|:----|:----|:----|:----|:----|:----|
|<mqueue.h>|•|•| |•|message queues|
|<spawn.h>|•|•|•|•|real-time spawn interface|

#### POSIX.1 optional interface groups and codes
|Code|SUS mandatory|Symbolic constant|Description|
|:----|:----|:----|:----|
|ADV| |_POSIX_ADVISORY_INFO|advisory information (real-time)|
|CPT| |_POSIX_CPUTIME|process CPU time clocks (real-time)|
|FSC|•|_POSIX_FSYNC|file synchronization|
|IP6| |_POSIX_IPV6|IPv6 interfaces|
|ML| |_POSIX_MEMLOCK|process memory locking (real-time)|
|MLR| |_POSIX_MEMLOCK_RANGE|memory range locking (real-time)|
|MON| |_POSIX_MONOTONIC_CLOCK|monotonic clock (real-time)|
|MSG| |_POSIX_MESSAGE_PASSING|message passing (real-time)|
|MX| |_ _STDC_IEC_559_ _|IEC 60559 floating-point option|
|PIO| |_POSIX_PRIORITIZED_IO|prioritized input and output|
|PS| |_POSIX_PRIORITY_SCHEDULING|process scheduling (real-time)|
|RPI| |_POSIX_THREAD_ROBUST_PRIO_INHERIT|robust mutex priority inheritance (real-time)|
|RPP| |_POSIX_THREAD_ROBUST_PRIO_PROTECT|robust mutex priority protection (real-time)|
|RS| |_POSIX_RAW_SOCKETS|raw sockets|
|SHM| |_POSIX_SHARED_MEMORY_OBJECTS|shared memory objects (real-time)|
|SIO| |_POSIX_SYNCHRONIZED_IO|synchronized input and output (real-time)|
|SPN| |_POSIX_SPAWN|spawn (real-time)|
|SS| |_POSIX_SPORADIC_SERVER|process sporadic server (real-time)|
|TCT| |_POSIX_THREAD_CPUTIME|thread CPU time clocks (real-time)|
|TPI| |_POSIX_THREAD_PRIO_INHERIT|nonrobust mutex priority inheritance (real-time)|
|TPP| |_POSIX_THREAD_PRIO_PROTECT|nonrobust mutex priority protection (real-time)|
|TPS| |_POSIX_THREAD_PRIORITY_SCHEDULING|thread execution scheduling (real-time)|
|TSA|•|_POSIX_THREAD_ATTR_STACKADDR|thread stack address attribute|
|TSH|•|_POSIX_THREAD_PROCESS_SHARED|thread process-shared synchronization|
|TSP| |_POSIX_THREAD_SPORADIC_SERVER|thread sporadic server (real-time)|
|TSS| |_POSIX_THREAD_ATTR_STACKSIZE|thread stack size address|
|TYM| |_POSIX_TYPED_MEMORY_OBJECTS|typed memory objects (real-time)|
|XSI|•|_XOPEN_UNIX|X/Open interfaces|

#### Sizes of integral values from <limits.h>

|Name|Description|Minimum acceptable value|Typical value|
|:----|:----|:----|:----|
|CHAR_BIT|bits in a char|8|8|
|CHAR_MAX|max value of char|(see later)|127|
|CHAR_MIN|min value of char|(see later)|−128|
|SCHAR_MAX|max value of signed char|127|127|
|SCHAR_MIN|min value of signed char|−127|−128|
|UCHAR_MAX|max value of unsigned char|255|255|
| | | | |
|INT_MAX|max value of int|32,767|2,147,483,647|
|INT_MIN|min value of int|−32,767|−2,147,483,648|
|UINT_MAX|max value of unsigned int|65,535|4,294,967,295|
| | | | |
|SHRT_MAX|max value of short|32,767|32,767|
|SHRT_MIN|min value of short|−32,767|−32,768|
|USHRT_MAX|max value of unsigned short|65,535|65,535|
| | | | |
|LONG_MAX|max value of long|2,147,483,647|2,147,483,647|
|LONG_MIN|min value of long|−2,147,483,647|−2,147,483,648|
|ULONG_MAX|max value of unsigned long|4294967295|4294967295|
| | | | |
|LLONG_MAX|max value of long long|9,223,372,036,854,780,000|9,223,372,036,854,780,000|
|LLONG_MIN|min value of long long|−9,223,372,036,854,775,807|−9,223,372,036,854,775,808|
|ULLONG_MAX|max value of unsigned long long|18,446,744,073,709,600,000|18,446,744,073,709,600,000|
| | | | |
|MB_LEN_MAX|max number of bytes in a multibyte character constant|1|6|

#### ISO limits on various platforms
|Limit|FreeBSD 8.0|Linux 3.2.0|Mac OS X 10.6.8|Solaris 10|
|:----|:----|:----|:----|:----|
|FOPEN_MAX|20|16|20|20|
|TMP_MAX|308,915,776|238,328|308,915,776|17,576|
|FILENAME_MAX|1,024|4,096|1,024|1,024|

#### POSIX.1 minimum values from <limits.h>
|Name|Description: minimum acceptable value for maximum ...|Value|
|:----|:----|:----|
|_POSIX_ARG_MAX|length of arguments to exec functions|4,096|
|_POSIX_CHILD_MAX|number of child processes at a time per real user ID|25|
|_POSIX_DELAYTIMER_MAX|number of timer expiration overruns|32|
|_POSIX_HOST_NAME_MAX|length of a host name as returned by gethostname|255|
|_POSIX_LINK_MAX|number of links to a file|8|
|_POSIX_LOGIN_NAME_MAX|length of a login name|9|
|_POSIX_MAX_CANON|number of bytes on a terminal’s canonical input queue|255|
|_POSIX_MAX_INPUT|space available on a terminal’s input queue|255|
|_POSIX_NAME_MAX|number of bytes in a filename, not including the terminating null|14|
|_POSIX_NGROUPS_MAX|number of simultaneous supplementary group IDs per process|8|
|_POSIX_OPEN_MAX|maximum number of open files per process|20|
|_POSIX_PATH_MAX|number of bytes in a pathname, including the terminating null|256|
|_POSIX_PIPE_BUF|number of bytes that can be written atomically to a pipe|512|
|_POSIX_RE_DUP_MAX|number of repeated occurrences of a basic regular expression permitted by the regexec and regcomp functions when using the interval notation \{m,n\}|255|
|_POSIX_RTSIG_MAX|number of real-time signal numbers reserved for applications|8|
|_POSIX_SEM_NSEMS_MAX|number of semaphores a process can have in use at one time|256|
|_POSIX_SEM_VALUE_MAX|value a semaphore can hold|32,767|
|_POSIX_SIGQUEUE_MAX|number of queued signals a process can send and have pending|32|
|_POSIX_SSIZE_MAX|value that can be stored in ssize_t object|32,767|
|_POSIX_STREAM_MAX|number of standard I/O streams a process can have open at once|8|
|_POSIX_SYMLINK_MAX|number of bytes in a symbolic link|255|
|_POSIX_SYMLOOP_MAX|number of symbolic links that can be traversed during pathname resolution|8|
|_POSIX_TIMER_MAX|number of timers per process|32|
|_POSIX_TTY_NAME_MAX|length of a terminal device name, including the terminating null|9|
|_POSIX_TZNAME_MAX|number of bytes for the name of a time zone|6|

#### POSIX.1 runtime invariant values from <limits.h>
|Name|Description|Minimum acceptable value|
|:----|:----|:----|
|ARG_MAX|maximum length of arguments to exec functions|_POSIX_ARG_MAX|
|ATEXIT_MAX|maximum number of functions that can be registered with the atexit function|32|
|CHILD_MAX|maximum number of child processes per real user ID|_POSIX_CHILD_MAX|
|DELAYTIMER_MAX|maximum number of timer expiration overruns|_POSIX_DELAYTIMER_MAX|
|HOST_NAME_MAX|maximum length of a host name as returned by gethostname|_POSIX_HOST_NAME_MAX|
|LOGIN_NAME_MAX|maximum length of a login name|_POSIX_LOGIN_NAME_MAX|
|OPEN_MAX|one more than the maximum value assigned to a newly created file descriptor|_POSIX_OPEN_MAX|
|PAGESIZE|system memory page size, in bytes|1|
|RTSIG_MAX|maximum number of real-time signals reserved for application use|_POSIX_RTSIG_MAX|
|SEM_NSEMS_MAX|maximum number of semaphores a process can use|_POSIX_SEM_NSEMS_MAX|
|SEM_VALUE_MAX|maximum value of a semaphore|_POSIX_SEM_VALUE_MAX|
|SIGQUEUE_MAX|maximum number of signals that can be queued for a process|_POSIX_SIGQUEUE_MAX|
|STREAM_MAX|maximum number of standard I/O streams a process can have open at once|_POSIX_STREAM_MAX|
|SYMLOOP_MAX|number of symbolic links that can be traversed during pathname resolution|_POSIX_SYMLOOP_MAX|
|TIMER_MAX|maximum number of timers per process|_POSIX_TIMER_MAX|
|TTY_NAME_MAX|length of a terminal device name, including the terminating null|_POSIX_TTY_NAME_MAX|
|TZNAME_MAX|number of bytes for the name of a time zone|_POSIX_TZNAME_MAX|

#### XSI minimum values from <limits.h>
|Name|Description|Minimum acceptable value|Typical value|
|:----|:----|:----|:----|
|NL_LANGMAX|maximum number of bytes in LANG environment variable|14|14|
|NZERO|default process priority|20|20|
|_XOPEN_IOV_MAX|maximum number of iovec structures that can be used with readv or writev|16|16|
|_XOPEN_NAME_MAX|number of bytes in a filename|255|255|
|_XOPEN_PATH_MAX|number of bytes in a pathname|1,024|1,024|

#### Limits and name arguments to sysconf
|Name of limit|Description|name argument|
|:----|:----|:----|
|ARG_MAX|maximum length, in bytes, of arguments to the exec functions|_SC_ARG_MAX|
|ATEXIT_MAX|maximum number of functions that can be registered with the atexit function|_SC_ATEXIT_MAX|
|CHILD_MAX|maximum number of processes per real user ID|_SC_CHILD_MAX|
|clock ticks/second|number of clock ticks per second|_SC_CLK_TCK|
|COLL_WEIGHTS_MAX|maximum number of weights that can be assigned to an entry of the LC_COLLATE order keyword in the locale definition file|_SC_COLL_WEIGHTS_MAX|
|DELAYTIMER_MAX|maximum number of timer expiration overruns|_SC_DELAYTIMER_MAX|
|HOST_NAME_MAX|maximum length of a host name as returned by gethostname|_SC_HOST_NAME_MAX|
|IOV_MAX|maximum number of iovec structures that can be used with readv or writev|_SC_IOV_MAX|
|LINE_MAX|maximum length of a utility’s input line|_SC_LINE_MAX|
|LOGIN_NAME_MAX|maximum length of a login name|_SC_LOGIN_NAME_MAX|
|NGROUPS_MAX|maximum number of simultaneous supplementary process group IDs per process|_SC_NGROUPS_MAX|
|OPEN_MAX|one more than the maximum value assigned to a newly created file descriptor|_SC_OPEN_MAX|
|PAGESIZE|system memory page size, in bytes|_SC_PAGESIZE|
|PAGE_SIZE|system memory page size, in bytes|_SC_PAGE_SIZE|
|RE_DUP_MAX|number of repeated occurrences of a basic regular expression permitted by the regexec and regcomp functions when using the interval notation \{m,n\}|_SC_RE_DUP_MAX|
|RTSIG_MAX|maximum number of real-time signals reserved for application use|_SC_RTSIG_MAX|
|SEM_NSEMS_MAX|maximum number of semaphores a process can use at one time|_SC_SEM_NSEMS_MAX|
|SEM_VALUE_MAX|maximum value of a semaphore|_SC_SEM_VALUE_MAX|
|SIGQUEUE_MAX|maximum number of signals that can be queued for a process|_SC_SIGQUEUE_MAX|
|STREAM_MAX|maximum number of standard I/O streams per process at any given time; if defined, it must have the same value as FOPEN_MAX|_SC_STREAM_MAX|
|SYMLOOP_MAX|number of symbolic links that can be traversed during pathname resolution|_SC_SYMLOOP_MAX|
|TIMER_MAX|maximum number of timers per process|_SC_TIMER_MAX|
|TTY_NAME_MAX|length of a terminal device name, including the terminating null|_SC_TTY_NAME_MAX|
|TZNAME_MAX|maximum number of bytes for a time zone name|_SC_TZNAME_MAX|

#### Limits and name arguments to pathconf and fpathconf
|Name of limit|Description|name argument|
|:----|:----|:----|
|FILESIZEBITS|minimum number of bits needed to represent, as a signed integer value, the maximum size of a regular file allowed in the specified directory|_PC_FILESIZEBITS|
|LINK_MAX|maximum value of a file’s link count|_PC_LINK_MAX|
|MAX_CANON|maximum number of bytes on a terminal’s canonical input queue|_PC_MAX_CANON|
|MAX_INPUT|number of bytes for which space is available on terminal’s input queue|_PC_MAX_INPUT|
|NAME_MAX|maximum number of bytes in a filename (does not include a null at end)|_PC_NAME_MAX|
|PATH_MAX|maximum number of bytes in a relative pathname, including the terminating null|_PC_PATH_MAX|
|PIPE_BUF|maximum number of bytes that can be written atomically to a pipe|_PC_PIPE_BUF|
|_POSIX_TIMESTAMP_RESOLUTION|_POSIX_TIMESTAMP_RESOLUTION resolution in nanoseconds for file timestamps|_PC_TIMESTAMP_RESOLUTION|
|SYMLINK_MAX|number of bytes in a symbolic link|_PC_SYMLINK_MAX|

#### Examples of configuration limits
|Limit|FreeBSD 8.0|Linux 3.2.0|Mac OS X 10.6.8|Solaris 10|Solaris 10|
|:----|:----|:----|:----|:----|:----|
| | | | |UFS file system|PCFS file system|
| | | | | | |
|ARG_MAX|262,144|2,097,152|262,144|2,096,640|2,096,640|
|ATEXIT_MAX|32|2,147,483,647|2,147,483,647|no limit|no limit|
|CHARCLASS_NAME_MAX|no symbol|2,048|14|14|14|
|CHILD_MAX|1,760|47,211|266|8,021|8,021|
|clock ticks/second|128|100|100|100|100|
|COLL_WEIGHTS_MAX|0|255|2|10|10|
|FILESIZEBITS|64|64|64|41|unsupported|
|HOST_NAME_MAX|255|64|255|255|255|
|IOV_MAX|1,024|1,024|1,024|16|16|
|LINE_MAX|2,048|2,048|2,048|2,048|2,048|
|LINK_MAX|32,767|65,000|32,767|32,767|1|
|LOGIN_NAME_MAX|17|256|255|9|9|
|MAX_CANON|255|255|1,024|256|256|
|MAX_INPUT|255|255|1,024|512|512|
|NAME_MAX|255|255|255|255|8|
|NGROUPS_MAX|1,023|65,536|16|16|16|
|OPEN_MAX|3,520|1,024|256|256|256|
|PAGESIZE|4,096|4,096|4,096|8,192|8,192|
|PAGE_SIZE|4,096|4,096|4,096|8,192|8,192|
|PATH_MAX|1,024|4,096|1,024|1,024|1,024|
|PIPE_BUF|512|4,096|512|5,120|5,120|
|RE_DUP_MAX|255|32,767|255|255|255|
|STREAM_MAX|3,520|16|20|256|256|
|SYMLINK_MAX|1,024|no limit|255|1,024|1,024|
|SYMLOOP_MAX|32|no limit|32|20|20|
|TTY_NAME_MAX|255|32|255|128|128|
|TZNAME_MAX|255|6|255|no limit|no limit|

#### Options and name arguments to pathconf and fpathconf
|Name of option|Indicates…|name argument|
|:----|:----|:----|
|_POSIX_CHOWN_RESTRICTED|whether use of chown is restricted|_PC_CHOWN_RESTRICTED|
|_POSIX_NO_TRUNC|whether filenames longer than NAME_MAX generate an error|_PC_NO_TRUNC|
|_POSIX_VDISABLE|if defined, terminal special characters can be disabled with this value|_PC_VDISABLE|
|_POSIX_ASYNC_IO|whether asynchronous I/O can be used with the associated file|_PC_ASYNC_IO|
|_POSIX_PRIO_IO|whether prioritized I/O can be used with the associated file|_PC_PRIO_IO|
|_POSIX_SYNC_IO|whether synchronized I/O can be used with the associated file|_PC_SYNC_IO|
|_POSIX2_SYMLINKS|whether symbolic links are supported in the directory|_PC_2_SYMLINKS|

#### Options and name arguments to sysconf
|Name of option|Indicates…|name argument|
|:----|:----|:----|
|_POSIX_ASYNCHRONOUS_IO|whether the implementation supports POSIX asynchronous I/O|_SC_ASYNCHRONOUS_IO|
|_POSIX_BARRIERS|whether the implementation supports barriers|_SC_BARRIERS|
|_POSIX_CLOCK_SELECTION|whether the implementation supports clock selection|_SC_CLOCK_SELECTION|
|_POSIX_JOB_CONTROL|whether the implementation supports job control|_SC_JOB_CONTROL|
|_POSIX_MAPPED_FILES|whether the implementation supports memory-mapped files|_SC_MAPPED_FILES|
|_POSIX_MEMORY_PROTECTION|whether the implementation supports memory protection|_SC_MEMORY_PROTECTION|
|_POSIX_READER_WRITER_LOCKS|whether the implementation supports reader–writer locks|_SC_READER_WRITER_LOCKS|
|_POSIX_REALTIME_SIGNALS|whether the implementation supports real-time signals|_SC_REALTIME_SIGNALS|
|_POSIX_SAVED_IDS|whether the implementation supports the saved set-user-ID and the saved set-group-ID|_SC_SAVED_IDS|
|_POSIX_SEMAPHORES|whether the implementation supports POSIX semaphores|_SC_SEMAPHORES|
|_POSIX_SHELL|whether the implementation supports the POSIX shell|_SC_SHELL|
|_POSIX_SPIN_LOCKS|whether the implementation supports spin locks|_SC_SPIN_LOCKS|
|_POSIX_THREAD_SAFE_FUNCTIONS|whether the implementation supports thread-safe functions|_SC_THREAD_SAFE_FUNCTIONS|
|_POSIX_THREADS|whether the implementation supports threads|_SC_THREADS|
|_POSIX_TIMEOUTS|whether the implementation supports timeout-based variants of selected functions|_SC_TIMEOUTS|
|_POSIX_TIMERS|whether the implementation supports timers|_SC_TIMERS|
|_POSIX_VERSION|the POSIX.1 version|_SC_VERSION|
|_XOPEN_CRYPT|whether the implementation supports the XSI encryption option group|_SC_XOPEN_CRYPT|
|_XOPEN_REALTIME|whether the implementation supports the XSI real-time option group|_SC_XOPEN_REALTIME|
|_XOPEN_REALTIME_THREADS|whether the implementation supports the XSI real-time threads option group|_SC_XOPEN_REALTIME_THREADS|
|_XOPEN_SHM|the XSI shared memory option group|_SC_XOPEN_SHM|
|_XOPEN_VERSION|the XSI version|_SC_XOPEN_VERSION|

#### Common primitive system data types
|Type|Description|
|:----|:----|
|clock_t|counter of clock ticks (process time) (Section 1.10)|
|comp_t|compressed clock ticks (not defined by POSIX.1; see Section 8.14)|
|dev_t|device numbers (major and minor) (Section 4.24)|
|fd_set|file descriptor sets (Section 14.4.1)|
|fpos_t|file position (Section 5.10)|
|gid_t|numeric group IDs|
|ino_t|i-node numbers (Section 4.14)|
|mode_t|file type, file creation mode (Section 4.5)|
|nlink_t|link counts for directory entries (Section 4.14)|
|off_t|file sizes and offsets (signed) (lseek, Section 3.6)|
|pid_t|process IDs and process group IDs (signed) (Sections 8.2 and 9.4)|
|pthread_t|thread IDs (Section 11.3)|
|ptrdiff_t|result of subtracting two pointers (signed)|
|rlim_t|resource limits (Section 7.11)|
|sig_atomic_t|data type that can be accessed atomically (Section 10.15)|
|sigset_t|signal set (Section 10.11)|
|size_t|sizes of objects (such as strings) (unsigned) (Section 3.7)|
|ssize_t|functions that return a count of bytes (signed) (read, write, Section 3.7)|
|time_t|counter of seconds of calendar time (Section 1.10)|
|uid_t|numeric user IDs|
|wchar_t|can represent all distinct character codes|

## 3. File I/O

### Function Prototypes

#### A file is opened or created by calling either the open function or the openat function.
```c
int	
open(const char *path, int oflag, ... /* mode_t mode */ );
	<fcntl.h>
	oflag: O_RDONLY, O_WRONLY, O_RDWR, O_EXEC, O_SEARCH; O_APPEND, O_CLOEXEC, O_CREAT, O_DIRECTORY, O_DSYNC, O_EXCL, O_NOCTTY, O_NOFOLLOW, O_NONBLOCK, O_RSYNC, O_SYNC, O_TRUNC, O_TTY_INIT
	mode: S_IS[UG]ID, S_ISVTX, S_I[RWX](USR|GRP|OTH)

int
openat(int fd, const char *path, int oflag, ... /* mode_t mode */ );
	<fcntl.h>
	oflag: O_RDONLY, O_WRONLY, O_RDWR, O_EXEC, O_SEARCH;
	O_APPEND, O_CLOEXEC, O_CREAT, O_DIRECTORY, O_DSYNC, O_EXCL, O_NOCTTY, O_NOFOLLOW, O_NONBLOCK, O_RSYNC, O_SYNC, O_TRUNC, O_TTY_INIT
	mode: S_IS[UG]ID, S_ISVTX, S_I[RWX](USR|GRP|OTH)
	Returns: file descriptor if OK, −1 on error
	Platforms: O_FSYNC flag on FreeBSD 8.0 and Mac OS X 10.6.8
```

#### A new file can also be created by calling the creat function.
```c
int
creat(const char *path, mode_t mode);
	<fcntl.h>
	mode: S_IS[UG]ID, S_ISVTX, S_I[RWX](USR|GRP|OTH)
	Returns: file descriptor opened for write-only if OK, −1 on error
```

#### An open file is closed by calling the close function.
```c
int
close(int fd);
	<unistd.h>
	Returns: 0 if OK, −1 on error
```

#### An open file’s offset can be set explicitly by calling lseek.
```c
off_t
lseek(int fd, off_t offset, int whence);
	<unistd.h>
	whence: SEEK_SET, SEEK_CUR, SEEK_END
	Returns: new file offset if OK, −1 on error
```

#### Data is read from an open file with the read function.
```c
ssize_t
read(int fd, void *buf, size_t nbytes);
	<unistd.h>
	Returns: number of bytes read if OK, 0 if end of file, −1 on error
```

#### Data is written to an open file with the write function.
```c
ssize_t
write(int fd, const void *buf, size_t nbytes);
	<unistd.h>
	Returns: number of bytes written if OK, −1 on error
```

#### The Single UNIX Specification includes two functions that allow applications to seek and perform I/O atomically: pread and pwrite.
```c
ssize_t
pread(int fd, void *buf, size_t nbytes, off_t offset);
	<unistd.h>
	Returns: number of bytes read, 0 if end of file, −1 on error

ssize_t
pwrite(int fd, const void *buf, size_t nbytes, off_t offset);
	<unistd.h>
	Returns: number of bytes written if OK, −1 on error
```

#### An existing file descriptor is duplicated by either of the following functions
```c
int
dup(int fd);
	<unistd.h>
	Returns: new file descriptor if OK, −1 on error

int
dup2(int fd, int fd2);
	<unistd.h>
	Returns: new file descriptor if OK, −1 on error
```

#### The kernel eventually writes all the delayed-write blocks to disk, normally when it needs to reuse the buffer for some other disk block. To ensure consistency of the file system on disk with the contents of the buffer cache, the sync, fsync, and fdatasync functions are provided.
```c
void
sync(void);
	<unistd.h>

int
fsync(int fd);
	<unistd.h>
	Returns: 0 if OK, −1 on error

int
fdatasync(int fd);
	<unistd.h>
	Returns: 0 if OK, −1 on error
	Platforms: Linux 3.2.0, Solaris 10
```

#### The fcntl function can change the properties of a file that is already open.
```c
int
fcntl(int fd, int cmd, ... /* int arg */ );
	<fcntl.h>
	cmd: F_DUPFD, F_DUPFD_CLOEXEC, F_GETFD, F_SETFD, F_GETFL, F_SETFL, F_GETOWN, F_SETOWN, F_GETLK, F_SETLK, F_SETLKW
	Returns: depends on cmd if OK, −1 on error
```

##### File status flags for fcntl
**F_GETFL**

Return the file status flags for fd as the value of the function.

Unfortunately, the five access-mode flags—O_RDONLY, O_WRONLY, O_RDWR, O_EXEC, and O_SEARCH—are not separate bits that can be tested. (As we mentioned earlier, the first three often have the values 0, 1, and 2, respectively, for historical reasons. Also, these five values are mutually exclusive; a file can have only one of them enabled.) Therefore, we must first use the O_ACCMODE mask to obtain the access-mode bits and then compare the result against any of the five values.

|File status flag|Description|
|:----|:----|
|O_RDONLY|open for reading only|
|O_WRONLY|open for writing only|
|O_RDWR|open for reading and writing|
|O_EXEC|open for execute only|
|O_SEARCH|open directory for searching only|
| | |
|O_APPEND|append on each write|
|O_NONBLOCK|nonblocking mode|
|O_SYNC|wait for writes to complete (data and attributes)|
|O_DSYNC|wait for writes to complete (data only)|
|O_RSYNC|synchronize reads and writes|
|O_FSYNC|wait for writes to complete (FreeBSD and Mac OS X only)|
|O_ASYNC|asynchronous I/O (FreeBSD and Mac OS X only)|

#### The ioctl function has always been the catchall for I/O operations. Anything that couldn’t be expressed using one of the other functions in this chapter usually ended up being specified with an ioctl. Terminal I/O was the biggest user of this function. (When we get to Chapter 18, we’ll see that POSIX.1 has replaced the terminal I/O operations with separate functions.)
```c
int
ioctl(int fd, int request, ...);
	<unistd.h>    /* System V */
	<sys/ioctl.h> /* BSD and Linux */
	Returns: −1 on error, something else if OK
```

### Examples

#### Test whether standard input is capable of seeking
```c
#include "apue.h"

int
main(void)
{
	if (lseek(STDIN_FILENO, 0, SEEK_CUR) == -1)
		printf("cannot seek\n");
	else
		printf("seek OK\n");
	exit(0);
}
```

```
./seek_segv < /etc/passwd		// seek OK
cat /etc/passwd | ./seek_segv	// cannot lseek
```

#### Create a file with a hole in it
```c
#include "apue.h"
#include <fcntl.h>

char	buf1[] = "abcdefghij";
char	buf2[] = "ABCDEFGHIJ";

int
main(void)
{
	int		fd;

	if ((fd = creat("file.hole", FILE_MODE)) < 0)
		err_sys("creat error");

	if (write(fd, buf1, 10) != 10)
		err_sys("buf1 write error");
	/* offset now = 10 */

	if (lseek(fd, 16384, SEEK_SET) == -1)
		err_sys("lseek error");
	/* offset now = 16384 */

	if (write(fd, buf2, 10) != 10)
		err_sys("buf2 write error");
	/* offset now = 16394 */

	exit(0);
}
```

```
./hole_segv 
od -c file.hole 
0000000   a   b   c   d   e   f   g   h   i   j  \0  \0  \0  \0  \0  \0
0000020  \0  \0  \0  \0  \0  \0  \0  \0  \0  \0  \0  \0  \0  \0  \0  \0
*
0040000   A   B   C   D   E   F   G   H   I   J
0040012
```

#### Copy standard input to standard output
```c
#include "apue.h"

#define BUFFSIZE	4096

int
main(void)
{
	int		n;
	char	buf[BUFFSIZE];

	while ((n = read(STDIN_FILENO, buf, BUFFSIZE)) > 0)
		if (write(STDOUT_FILENO, buf, n) != n)
			err_sys("write error");

	if (n < 0)
		err_sys("read error");

	exit(0);
}
```

#### Print file flags for specified descriptor
```c
#include "apue.h"
#include <fcntl.h>

int
main(int argc, char *argv[])
{
	int		val;

	if (argc != 2)
		err_quit("usage: a.out <descriptor#>");

	if ((val = fcntl(atoi(argv[1]), F_GETFL, 0)) < 0)
		err_sys("fcntl error for fd %d", atoi(argv[1]));

	switch (val & O_ACCMODE) {
	case O_RDONLY:
		printf("read only");
		break;

	case O_WRONLY:
		printf("write only");
		break;

	case O_RDWR:
		printf("read write");
		break;

	default:
		err_dump("unknown access mode");
	}

	if (val & O_APPEND)
		printf(", append");
	if (val & O_NONBLOCK)
		printf(", nonblocking");
	if (val & O_SYNC)
		printf(", synchronous writes");

#if !defined(_POSIX_C_SOURCE) && defined(O_FSYNC) && (O_FSYNC != O_SYNC)
	if (val & O_FSYNC)
		printf(", synchronous writes");
#endif

	putchar('\n');
	exit(0);
}
```

#### Turn on one or more of the file status flags for a descriptor
```c
#include "apue.h"
#include <fcntl.h>

void
set_fl(int fd, int flags) /* flags are file status flags to turn on */
{
	int		val;

	if ((val = fcntl(fd, F_GETFL, 0)) < 0)
		err_sys("fcntl F_GETFL error");

	val |= flags;		/* turn on flags */

	if (fcntl(fd, F_SETFL, val) < 0)
		err_sys("fcntl F_SETFL error");
}
```

#### Turn off one or more of the file status flags for a descriptor
```c
#include "apue.h"
#include <fcntl.h>

void
clr_fl(int fd, int flags) /* flags are file status flags to turn on */
{
	int		val;

	if ((val = fcntl(fd, F_GETFL, 0)) < 0)
		err_sys("fcntl F_GETFL error");

	val &= ~flags;		/* turn on flags */

	if (fcntl(fd, F_SETFL, val) < 0)
		err_sys("fcntl F_SETFL error");
}

```

#### Implementation of dup2 without using fcntl
```c
#include "apue.h"
#include <errno.h>

int
dup2(int fd, int fd2)
{
    long openmax;
    int savederr, idx;
    int *tfd;

    if (fd == fd2)
        return(fd);
    if ((openmax = open_max()) < 0)
        return(-1);
    if (fd2 < 0 || fd2 >= openmax) {
        errno = EBADF;
        return(-1);
    }
    if ((tfd = malloc(openmax * sizeof(int))) == NULL)
        return(-1);
    close(fd2);

    savederr = 0;
    idx = 0;
    while (idx < openmax) {
        if ((tfd[idx] = dup(fd)) < 0) {
            savederr = errno;
            break;
        }
        if (tfd[idx] == fd2)
            break;
        idx++;
    }
    if (idx >= openmax)
        savederr = EMFILE;
    while (--idx >= 0)
        close(tfd[idx]);
    free(tfd);
    errno = savederr;
    if (errno != 0)
        exit(-1);
    else
        return(fd2);
}
```

```c
#include "apue.h"
#include <limits.h>
#include <sys/resource.h>

#define OPEN_MAX_GUESS	256

long
open_max(void)
{
	long openmax;
	struct rlimit rl;

	if ((openmax = sysconf(_SC_OPEN_MAX)) < 0 ||
	  openmax == LONG_MAX) {
		if (getrlimit(RLIMIT_NOFILE, &rl) < 0)
			err_sys("can't get file limit");
		if (rl.rlim_max == RLIM_INFINITY)
			openmax = OPEN_MAX_GUESS;
		else
			openmax = rl.rlim_max;
	}
	return(openmax);
}
```

#### Determine the size of a disk device
```c
#include "apue.h"
#include <fcntl.h>
#include <errno.h>
#include <limits.h>

#ifndef NBPSCTR
#define NBPSCTR 512 /* number of bytes per sector */
#endif

#define KB 1024L
#define MB (KB*KB)
#define GB (KB*MB)
#define TB (KB*GB)
#define KBF 1024.
#define MBF (KBF*KBF)
#define GBF (KBF*MBF)
#define TBF (KBF*GBF)

char buf[NBPSCTR];

off_t disksize(int);

int
main(int argc, char *argv[])
{
    int         fd;
    off_t       disksz;
    char        *device;
    struct stat sbuf;

    /* usage */
    if (argc != 2)
        err_quit("usage: dksz device");

    /* open */
    device = argv[1];
    if ((fd = open(device, O_RDONLY)) < 0)
        err_sys("dksz: can't open device %s", device);

    /* stat */
    if (fstat(fd, &sbuf) < 0)
        err_sys("dksz: can't stat device %s", device);

    /* check if blk/chr device */
    if (!S_ISBLK(sbuf.st_mode) && !S_ISCHR(sbuf.st_mode))
        err_quit("dksz: %s is not a device special file", device);

    /* get size of disk partition */
    disksz = disksize(fd);
    if (disksz >= TB)
        printf("%.2f TB\n", disksz / TBF);
    else if (disksz >= GB)
        printf("%.2f GB\n", disksz / GBF);
    else if (disksz >= MB)
        printf("%.2f MB\n", disksz / MBF);
    else if (disksz >= KB)
        printf("%.2f KB\n", disksz / KBF);
    else
        printf("%ld bytes\n", (long)disksz);
    exit(0);
}

/* 
 * Find the size of a disk partition using a binary search.
 */
off_t
disksize(int fd)
{
    int     n;
    off_t   maxsctr, upper, lower, o;

    /* size off_t */
    if (sizeof(off_t) > 4)
        maxsctr = 0x7fffffffffffffffLL;
    else
        maxsctr = 0x7fffffff;

    lower = 0;
    upper = maxsctr / NBPSCTR;
    for (;;) {
        o = upper * NBPSCTR;
        if (lseek(fd, o, SEEK_SET) == -1L) {
            upper = lower + (upper - lower) / 2;
            continue;
        }

        n = read(fd, buf, NBPSCTR);
        if (n > 0) {
            if (upper == maxsctr)
                return(o);

            lower = upper;
            upper *= 2;
            if (upper > maxsctr || upper <= lower)
                upper = maxsctr;
        }   else if (n == 0) {
#ifdef MACOS
            /* For some reason, MacOS X can return 0 past
             * EOF on some (4KB?) boundaries. We need to
             * verify that we're really at EOF by reading
             * the preceding block. */
                if (o != 0) {
                    if (lseek(fd, o-NBPSCTR, SEEK_SET) == -1L) {
                        upper = lower + (upper - 1 - lower) / 2;
                        continue;
                    }
                }
#endif
            return(o);
        } else {
            upper = lower + (upper - lower) / 2;
        }
    }
}
```

### Tables

#### Size in bytes of off_t for different platforms
|Operating system|CPU architecture|FILE_OFFSET_BITS value| | |
|:----|:----|:----|:----|:----|
| | |Undefined|32|64|
| | | | | |
|FreeBSD 8.0|x86 32-bit|8|8|8|
|Linux 3.2.0|x86 64-bit|8|8|8|
|Mac OS X 10.6.8|x86 64-bit|8|8|8|
|Solaris 10|SPARC 64-bit|8|4|8|

#### Timing results for reading with different buffer sizes on Linux
|BUFFSIZE|User CPU (seconds)|System CPU (seconds)|Clock time (seconds)|Number of loops|
|:----|:----|:----|:----|:----|
|1|20.03|117.50|138.73|516,581,760|
|2|9.69|58.76|68.60|258,290,880|
|4|4.60|36.47|41.27|129,145,440|
|8|2.47|15.44|18.38|64,572,720|
|16|1.07|7.93|9.38|32,286,360|
|32|0.56|4.51|8.82|16,143,180|
|64|0.34|2.72|8.66|8,071,590|
|128|0.34|1.84|8.69|4,035,795|
|256|0.15|1.30|8.69|2,017,898|
|512|0.09|0.95|8.63|1,008,949|
|1,024|0.02|0.78|8.58|504,475|
|2,048|0.04|0.66|8.68|252,238|
|4,096|0.03|0.58|8.62|126,119|
|8,192|0.00|0.54|8.52|63,060|
|16,384|0.01|0.56|8.69|31,530|
|32,768|0.00|0.56|8.51|15,765|
|65,536|0.01|0.56|9.12|7,883|
|131,072|0.00|0.58|9.08|3,942|
|262,144|0.00|0.60|8.70|1,971|
|524,288|0.01|0.58|8.58|986|

#### Linux ext4 timing results using various synchronization mechanisms
|Operation|User CPU (seconds)|System CPU (seconds)|Clock time (seconds)|
|:----|:----|:----|:----|
|read time from Figure 3.6 for BUFFSIZE = 4,096|0.03|0.58|8.62|
|normal write to disk file|0.00|1.05|9.70|
|write to disk file with O_SYNC set|0.02|1.09|10.28|
|write to disk followed by fdatasync|0.02|1.14|17.93|
|write to disk followed by fsync|0.00|1.19|18.17|
|write to disk with O_SYNC set followed by fsync|0.02|1.15|17.88|

#### Common FreeBSD ioctl operations
|Category|Constant names|Header|Number of ioctls|
|:----|:----|:----|:----|
|disk labels|DIOxxx|<sys/disklabel.h>|4.00|
|file I/O|FIOxxx|<sys/filio.h>|14.00|
|mag tape I/O|MTIOxxx|<sys/mtio.h>|11.00|
|socket I/O|SIOxxx|<sys/sockio.h>|73.00|
|terminal I/O|TIOxxx|<sys/ttycom.h>|43.00|

## 4. Files and Directories <<< CONTINUE HERE  (PAGE 93) <<<

### Function Prototypes

### Examples

### Tables

## 5. Standard I/O Library

### Function Prototypes

### Examples

### Tables

## 6. System Data Files and Information

### Function Prototypes

### Examples

### Tables

## 7. Process Environment

### Function Prototypes

### Examples

### Tables

## 8. Process Control

### Function Prototypes

### Examples

### Tables

## 9. Process Relationships

### Function Prototypes

### Examples

### Tables

## 10. Signals

### Function Prototypes

### Examples

### Tables

## 11. Threads

### Function Prototypes

### Examples

### Tables

## 12. Thread Control

### Function Prototypes

### Examples

### Tables

## 13. Daemon Processes

### Function Prototypes

### Examples

### Tables

## 14. Advanced I/O

### Function Prototypes

### Examples

### Tables

## 15. Interprocess Communication

### Function Prototypes

### Examples

### Tables

## 16. Network IPC: Sockets

### Function Prototypes

### Examples

### Tables

## 17. Advanced IPC

### Function Prototypes

### Examples

### Tables

## 18. Terminal I/O

### Function Prototypes

### Examples

### Tables

## 19. Pseudo Terminals

### Function Prototypes

### Examples

### Tables

## 20. A Database Library

### Function Prototypes

### Examples

### Tables

## 21. Communicating with a Network Printer

### Function Prototypes

### Examples

### Tables

## Appendix A - Library and Function Notes

### <netdb.h>

### <poll.h>

### <pthread.h>

### <pwd.h>

### <semaphore.h>

### <setjmp.h>

### <shadow.h>

### <siginfo.h>

### <signal.h>

### <stdio.h>

#### fputc(), fputs(), putc(), putchar(), puts()
![[05 PROGRAMMING/C#Print file flags for specified descriptor]]

### <stdarg.h>

### <stdlib.h>

#### atoi(), atol(), atoll()
![[05 PROGRAMMING/C#Print file flags for specified descriptor]]

#### exit()
Exit codes:
```
-   exit(1):		It indicates abnormal termination of a program perhaps as a result a minor problem in the code.
-   exit(2):		It is similar to exit(1) but is displayed when the error occurred is a major one. This statement is rarely seen.
-   exit(127):		It indicates command not found.
-   exit(132):		It indicates that a program was aborted (received [SIGILL],  perhaps as a result of illegal instruction or that the binary is probably corrupt.
-   exit(133):		It indicates that a program was aborted (received [SIGTRAP], perhaps as a result of dividing an integer by zero.
-   exit(134):		It indicates that a program was aborted (received [SIGABRT], perhaps as a result of a failed assertion.
-   exit(136):		It indicates that a program was aborted (received [SIGFPE],  perhaps as a result of floating point exception or integer overflow.
-   exit(137):		It indicates that a program took up too much memory.
-   exit(138):		It indicates that a program was aborted, perhaps as a result of unaligned memory access.
-   exit(139):		It indicates Segmentation Fault which means that the program was trying to access a memory location not allocated to it. This mostly occurs while using pointers or trying to access an out-of-bounds array index.
-   exit(158/152):	It indicates that a program was aborted (received SIGXCPU), perhaps as a result of CPU time limit exceeded.
-   exit(159/153):	It indicates that a program was aborted (received SIGXFSZ), perhaps as a result of File size limit exceeded.
```

### <string.h>

### <syslog.h>

### <sys/ipc.h>

### <sys/msg.h>

### <sys/mman.h>

### <sys/resource.h>

### <sys/select.h>

### <sys/sem.h>

### <sys/shm.h>

### <sys/socket.h>

### <sys/stat.h>

### <syslog.h>

### <sys/time.h>

### <sys/types.h>

### <sys/uio.h>

### <sys/utsname.h>

### <sys/wait.h>

### <termios.h>

### <time.h>

### <unistd.h>		

#### exec(), execl(), execlp(), execle(), execv(), execvp(), execvpe()
Difference between functions:
```
Since all of these function belongs to exec() family, let me `differentiate` according to `extra characters` with the meanings,

execve()
	v   argument will be passed as `array`
	e   environment will be taken from `envp argument`

execle()
	l	argument will be passed as `list`
	e   environment will be taken from `envp argument`

execlp()
	l   argument will be passed as `list`
	p   name of the program to run will be taken from `filename` specified or system will `search for program file` in `PATH` variable.

execvp()
	v   argument will be passed as `array`
	p   name of the program to run will be taken from `filename` specified or system will `search for program file` in `PATH` variable.

execv()
	v   argument will be passed as `array`

execl()
	l   argument will be passed as `list`
```

### <wchar.h>

# References
----

