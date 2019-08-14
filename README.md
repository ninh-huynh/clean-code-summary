This is the summary of Clean Code

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