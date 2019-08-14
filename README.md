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