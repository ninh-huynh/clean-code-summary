This is the summary of Clean Code

# TABLE OF CONTENT
- [Chapter 01: Clean Code](#Chapter-1:-Clean-Code)
  - [There will be code](#There-will-be-code)
  - [Bad code](#Bad-code)
  - [The total cost of owning a mess](#The-total-cost-of-owning-a-mess)
  - [Schools of Thought](#Schools-of-Thought)
  - [We are authors](#We-are-authors)
  - [The boy scout rule](#The-boy-scout-rule)
  - [Prequel and Principles](#Prequel-and-Principles)
  - [Conclusion](#Conclusion)
  - [Bibiography](#Bibiography)
- [Chapter 02: Meaningful Names](#Chapter-2:-Meaningful-Names)
  - [1. Use Intention-Revealing Names](#1.-Use-Intention-Revealing-Names)
  - [2. Avoid disinfomation](#2.-Avoid-disinfomation)
  - [3. Make meaningful Distinctions](#3.-Make-meaningful-Distinctions)
  - [4. Use pronounceable names](#4.-Use-pronounceable-names)
  - [5. Use searchable names](#5.-Use-searchable-names)
  - [6. Avoid Encodings](#6.-Avoid-Encodings)
  - [7. Avoid mental mapping](#7.-Avoid-mental-mapping)
  - [8. Class names](#8.-Class-names)
  - [9. Method names](#9.-Method-names)
  - [10. Don't be cute](#10.-Don't-be-cute)
  - [11. Pick one word per concept](#11.-Pick-one-word-per-concept)
  - [12. Don't pun](#12.-Don't-pun)
  - [13. Use solution domain names](#13.-Use-solution-domain-names)
  - [14. Use problem domain names](#14.-Use-problem-domain-names)
  - [15. Add meaningful context](#15.-Add-meaningful-context)
  - [16. Don't add gratutious context](#16.-Don't-add-gratutious-context)
  - [17. Final words](#17.-Final-words)
- [Chapter 03 Functions](#Chapter-3:-Functions)
  - [1. Small](#1.-Small)
  - [2. Do one thing](#2.-Do-one-thing)
  - [3. One level of abstraction per function](#3.-One-level-of-abstraction-per-function)
  - [4. Switch statments](#4.-Switch-statments)
  - [5. Use descriptive names](#5.-Use-descriptive-names)
  - [6. Function Arguments](#6.-Function-Arguments)
  - [7. Have no side effects](#7.-Have-no-side-effects)
  - [8. Command Query Separation](#8.-Command-Query-Separation)
  - [9. Prefer Exceptions to Returning Error codes](#9.-Prefer-Exceptions-to-Returning-Error-codes)
  - [10. Don't Repeat Yourself](#10.-Don't-Repeat-Yourself)
  - [11. Structured Programming](#11.-Structured-Programming)

- [Chapter 04: Comments](#chapter-4-comments)
  - []()
# Chapter 1: Clean Code
## There will be code
Code is really the language in which we ulitmately express the requirements.

## Bad code
## The total cost of owning a mess
## Schools of Thought
## We are authors
## The boy scout rule
## Prequel and Principles
## Conclusion
## Bibiography

# Chapter 2: Meaningful Names
## 1. Use Intention-Revealing Names

### Ex1: 
```java
int elapsedTimeInDays;
int daysSinceCreation;
int daysSinceModification;
int fileAgeInDays;
```

### Ex2:

Before:
```java
public List<int[]> getThem() {
    List<int[]> list1 = new ArrayList<int[]>();
    for (int[] x : theList)
        if (x[0] == 4)
            list1.add(x);
    return list1;
}
```

After:
```java
public List<int[]> getFlaggedCells() {
    List<int[]> flaggedCells = new ArrayList<int[]>();
    for (int[] cell : gameBoard)
        if (cell[STATUS_VALUE] == FLAGGED)
            flaggedCells.add(cell);
    return flaggedCells;
}
```

or even better, create a Cell class
```java
public List<Cell> getFlaggedCells() {
    List<Cell> flaggedCells = new ArrayList<Cell>();
    for (Cell cell : gameBoard)
        if (cell.isFlagged())
            flaggedCells.add(cell);
    return flaggedCells;
}
```

## 2. Avoid disinfomation
- Avoid leaving false clue that obscure the meaning of code: `hp`, `aix`, `sco`.
- Avoid use lower-case `L` or upper-case `o` as variable names.

## 3. Make meaningful Distinctions
- Number-serires naming `(a1, a2,..., aN)` are noninformative
- Noise words are meaningless distinction: `ProductInfo`, `ProductData`
- `variable` should never appear in a variable name
- `table` should never appear in a table name
- `Name` is alway better than `NameString`

## 4. Use pronounceable names
Before:
```java
class DtaRcrd102 {
    private Date genymdhms;
    private Date modymdhms;
    private final String pszqint = "102";
    /* ... */
};
```

After:
```java
class Customer {
    private Date generationTimestamp;
    private Date modificationTimestamp;;
    private final String recordId = "102";
/* ... */
};
```

## 5. Use searchable names
- Single-letter names can ONLY used as local variables.
- The length of a name should correspond to the size of its scope.

Before:
```java
for (int j = 0; j < 34; j++){
    s += (t[j] * 4) / 5;
}
```

After:
```java
int realDaysPerIdealday = 4;
const int WORK_DAYS_PER_WEEK = 5;
int sum = 0;
for (int j = 0; j < NUMBER_OF_TASKS; j++){
    int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
    int realTaskWeeks = (realdays / WORK_DAYS_PER_WEEK);
    sum += realTaskWeeks;
}
```

## 6. Avoid Encodings
### Hungarian Notation
### Member Prefixes
From this
```java
public class Part {
    private String m_dsc; // The textual description
    void setName(String name) {
        m_dsc = name;
    }
}
```
To:
```java
public class Part {
    String description;
    void setDescription(String description) {
        this.description = description;
    }
}
```
### Interfaces and Implementations
We must encode either interface or the implementation.
Ex: `IShapeFactory`, `ShapeFactory` or `ShapeFactory`, `ShapeFactoryImp`

## 7. Avoid mental mapping
- Use single-letter variable names for a loop counter if its scope is very small

## 8. Class names
- Should have noun or noun pharse names.
Ex: `Customer`, `WikiPage`, `Account`.
- Avoid words like: `Manager`, `Processor`, `Data`, `Info`.
- Should not be a verb.

## 9. Method names
- Should have verb or verb pharse name. Ex: `postPayment`, `deletePage`, `save`.
- Accessors, mutators, predicates should be named for their value, prefixed with `get`, `set`, `is`.
```java
String name = employee.getName();
customer.setName("mike");
if (paycheck.isPosted())...
```
- Use static factory method with names that describe the arguments when constructors are overloaded.
```java
Complex fullcrumPoint =  Complex.FromRealNumber(23.0);
```
## 10. Don't be cute
## 11. Pick one word per concept
## 12. Don't pun
## 13. Use solution domain names
## 14. Use problem domain names
- Use the name from problem domain when there is no "programmer-eese" for what we're doing.

## 15. Add meaningful context
## 16. Don't add gratutious context
## 17. Final words
- Choosing good names requires good descriptive skills and a shared cultural background

# Chapter 3: Functions
## 1. Small
- Function should be small
- _They should be smaller than that_
- Function should hardly ever be 20 lines long.

## 2. Do one thing
- _FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY._

## 3. One level of abstraction per function
## 4. Switch statments
- Bury the `switch` statment in the basement of an ABSTRACT FACTORY
- Create polymorphic objects, hidden behind an inheritance relationship

## 5. Use descriptive names
- Don't be afraid to make a name long.
- Don't be afraid to spend time choosing a name.
- Use the same pharases, nouns, and verbs in the function name

## 6. Function Arguments
- Three arguments (triadic) should be avoided where possible
- Using an output argument instead of a return value for a transformation is confusing.
- Flag arguments are ugly => Split the function into two


## 7. Have no side effects

## 8. Command Query Separation

Functions should either do something or answer something, but not both.

## 9. Prefer Exceptions to Returning Error codes
Turn this
```java
if (deletePage(page) == E_OK) {
    if (registry.deleteReference(page.name) == E_OK) {
        if (configKeys.deleteKey(page.name.makeKey()) == E_OK){
            logger.log("page deleted");
        } else {
            logger.log("configKey not deleted");
        }
    } else {
    logger.log("deleteReference from registry failed");
    }
} else {
    logger.log("delete failed");
    return E_ERROR;
}
```

to this

```java
try {
    deletePage(page);
    registry.deleteReference(page.name);
    configKeys.deleteKey(page.name.makeKey());
} 
catch (Exception e) {
    logger.log(e.getMessage());
}
```
## 10. Don't Repeat Yourself

Duplication may be the root of all evil in software

## 11. Structured Programming

Dijkstra said that every function, and every block within a function, should have one entry and one exit

It mean that there should only be one return statement in a function, no `break` or `continue` statments in a loop, and never, _ever_, any `goto` statements.

# Chapter 4: Comments
## Comments do not make up for bad code
- Rather than spend our time writing the comments that explain the mess we have made, spend it cleaning that mess.

## Explain yourself in code
Bad:

```java
// Check to see if the employee is eligible for full benefits
if ((employee.flags & HOURLY_FLAG) &&
    (employee.age > 65))
```

Good:
```java
if (employee.isEligibleForFullBenefits())
```


## Good comments
### Legal comments
 Where posssoble, refer to standard license or other external document
```java
// Copyright (C) 2003,2004,2005 by Object Mentor, Inc. All rights reserved.
// Released under the terms of the GNU General Public License version 2 or later.
```
### Informative Comments
```java
// format matched kk:mm:ss EEE, MMM dd, yyyy
Pattern timeMatcher = Pattern.compile(
"\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*");
```
### Explanation of Intent
```java
public void testConcurrentAddWidgets() throws Exception {
    WidgetBuilder widgetBuilder =
        new WidgetBuilder(new Class[]{BoldWidget.class});
    String text = "'''bold text'''";
    ParentWidget parent =
        new BoldWidget(new MockWidgetRoot(), "'''bold text'''");
    AtomicBoolean failFlag = new AtomicBoolean();
    failFlag.set(false);
    //This is our best attempt to get a race condition
    //by creating large number of threads.
    for (int i = 0; i < 25000; i++) {
        WidgetBuilderThread widgetBuilderThread =
            new WidgetBuilderThread(widgetBuilder, text, parent, failFlag);
        Thread thread = new Thread(widgetBuilderThread);
        thread.start();
    }
    assertEquals(false, failFlag.get());
}
```


### Clarification
```java
public void testCompareTo() throws Exception
{
    WikiPagePath a = PathParser.parse("PageA");
    WikiPagePath ab = PathParser.parse("PageA.PageB");
    WikiPagePath b = PathParser.parse("PageB");
    WikiPagePath aa = PathParser.parse("PageA.PageA");
    WikiPagePath bb = PathParser.parse("PageB.PageB");
    WikiPagePath ba = PathParser.parse("PageB.PageA");
    assertTrue(a.compareTo(a) == 0);    // a == a    
    assertTrue(a.compareTo(b) != 0);    // a != b
    assertTrue(ab.compareTo(ab) == 0);  // ab == ab
    assertTrue(a.compareTo(b) == -1);   // a < b
    assertTrue(aa.compareTo(ab) == -1); // aa < ab
    assertTrue(ba.compareTo(bb) == -1); // ba < bb
    assertTrue(b.compareTo(a) == 1);    // b > a
    assertTrue(ab.compareTo(aa) == 1);  // ab > aa
    assertTrue(bb.compareTo(ba) == 1);  // bb > ba
}
```

### Warning of Consequences
 We can turn off the test case by using the `@Ignore` attribute. Ex: `@Ignore("Takes too long to run")`.


```java
public static SimpleDateFormat makeStandardHttpDateFormat()
{
    //SimpleDateFormat is not thread safe,
    //so we need to create each instance independently.
    SimpleDateFormat df = new SimpleDateFormat("EEE, dd MMM yyyy HH:mm:ss z");
    df.setTimeZone(TimeZone.getTimeZone("GMT"));
    return df;
}
```
### TODO Comments
```java
//TODO-MdM these are not needed
// We expect this to go away when we do the checkout model
protected VersionInfo makeVersion() throws Exception
{
    return null;
}
```
### Amplification
```java
String listItemContent = match.group(3).trim();
// the trim is real important. It removes the starting
// spaces that could cause the item to be recognized
// as another list.
new ListItemWidget(this, listItemContent, this.level + 1);
return buildList(text.substring(match.end()));
```
### Javadocs in Public APIs

## Bad comments

### Mumbling

### Redundant Comments
```java
// Utility method that returns when this.closed is true. Throws an exception
// if the timeout is reached.
public synchronized void waitForClose(final long timeoutMillis)
throws Exception
{
    if (!closed)
    {
        wait(timeoutMillis);
        if (!closed)
            throw new Exception("MockResponseSender could not be closed");
    }
}
```

### Misleading comments

### Mandated comments
```java
/**
*
* @param title The title of the CD
* @param author The author of the CD
* @param tracks The number of tracks on the CD
* @param durationInMinutes The duration of the CD in minutes
*/
public void addCD(String title, String author,
                    int tracks, int durationInMinutes) {
    CD cd = new CD();
    cd.title = title;
    cd.author = author;
    cd.tracks = tracks;
    cd.duration = duration;
    cdList.add(cd);
}
```

### Journal Comments
```java
/*
*
* Changes (from 11-Oct-2001)
* --------------------------
* 11-Oct-2001 : Re-organised the class and moved it to new package
* com.jrefinery.date (DG);
* 05-Nov-2001 : Added a getDescription() method, and eliminated NotableDate
* class (DG);
* 12-Nov-2001 : IBD requires setDescription() method, now that NotableDate
* class is gone (DG); Changed getPreviousDayOfWeek(),
* getFollowingDayOfWeek() and getNearestDayOfWeek() to correct
* bugs (DG);
* 05-Dec-2001 : Fixed bug in SpreadsheetDate class (DG);
* 29-May-2002 : Moved the month constants into a separate interface
* (MonthConstants) (DG);
* 27-Aug-2002 : Fixed bug in addMonths() method, thanks to N???levka Petr (DG);
* 03-Oct-2002 : Fixed errors reported by Checkstyle (DG);
* 13-Mar-2003 : Implemented Serializable (DG);
* 29-May-2003 : Fixed bug in addMonths method (DG);
* 04-Sep-2003 : Implemented Comparable. Updated the isInRange javadocs (DG);
* 05-Jan-2005 : Fixed bug in addYears() method (1096282) (DG);
*/
```

### Noise Comments

```java
/**
* Default constructor.
*/
protected AnnualDateRule() {
}
```

```java
/** The day of the month. */
private int dayOfMonth;
```

```java
/**
* Returns the day of the month.
*
* @return the day of the month.
*/
public int getDayOfMonth() {
return dayOfMonth;
}
```

### Scary noise
```java
/** The name. */
private String name;
/** The version. */
private String version;
/** The licenceName. */
private String licenceName;
/** The version. */
private String info;
```

### Don't use a comment when you can use a function or a variable
Bad:
```java
// does the module from the global list <mod> depend on the
// subsystem we are part of?
if (smodule.getDependSubsystems().contains(subSysMod.getSubSystem()))
```

Good:
```java
ArrayList moduleDependees = smodule.getDependSubsystems();
String ourSubSystem = subSysMod.getSubSystem();
if (moduleDependees.contains(ourSubSystem))
```

### Position markers

### Closing brace comments
> If you find yourself wanting to mark your closing braces, try to shorten your functions instead.

### Attributions and Bylines
Source code control system is a better place for this kind of information.

### Commented-Out code
Don't do this:
```java
InputStreamResponse response = new InputStreamResponse();
response.setBody(formatter.getResultStream(), formatter.getByteCount());
// InputStream resultsStream = formatter.getResultStream();
// StreamReader reader = new StreamReader(resultsStream);
// response.setContent(reader.read(formatter.getByteCount()));
```

### HTML Comments

### Nonlocal Information
```java
/**
* Port on which fitnesse would run. Defaults to <b>8082</b>.
*
* @param fitnessePort
*/
public void setFitnessePort(int fitnessePort)
{
    this.fitnessePort = fitnessePort;
}
```

### Too much information
Don't put interseting historical discussions/irrelevant description into comments
```java
/*
RFC 2045 - Multipurpose Internet Mail Extensions (MIME)
Part One: Format of Internet Message Bodies
section 6.8. Base64 Content-Transfer-Encoding
The encoding process represents 24-bit groups of input bits as output
strings of 4 encoded characters. Proceeding from left to right, a
24-bit input group is formed by concatenating 3 8-bit input groups.
These 24 bits are then treated as 4 concatenated 6-bit groups, each
of which is translated into a single digit in the base64 alphabet.
When encoding a bit stream via the base64 encoding, the bit stream
must be presumed to be ordered with the most-significant-bit first.
That is, the first bit in the stream will be the high-order bit in
the first 8-bit byte, and the eighth bit will be the low-order bit in
the first 8-bit byte, and so on.
*/
```

### Inobvious connection
```java
/*
* start with an array that is big enough to hold all the pixels
* (plus filter bytes), and an extra 200 bytes for header info
*/
this.pngBytes = new byte[((this.width + 1) * this.height * 3) + 200];
```

### Function Headers

### Javadocs in Nonpublic code

# Chapter 5. Formatting

## The purpose of formatting
Code formatting is about communication, and communication is the professional developer's first order of business.

## Vertical formatting
- It possible to build significant systems out of files that are typically 200 lines long, with an upper limit of 500.
- It should be considered very desirable.

### Variable declarations
Variables should be declared as close to their usage as possible.

### Dependent functions
If one function calls another, they should be vertically close and the caller should be abobe the callee, if at all possible.

## Horizontal formatting
## Team rules
## Uncle Bob's formatting rules