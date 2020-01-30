# Code smells

## Principle

In computer programming, a code smell is any characteristic in the source code of a program that possibly indicates a deeper problem. Determining what is and is not a code smell is subjective, and varies by language, developer, and development methodology.

The term was popularised by Kent Beck on WardsWiki in the late 1990s. Usage of the term increased after it was featured in the book Refactoring: Improving the Design of Existing Code by Martin Fowler. It is also a term used by agile programmers.

One way to look at smells is with respect to principles and quality: "Smells are certain structures in the code that indicate violation of fundamental design principles and negatively impact design quality". Code smells are usually not bugs; they are not technically incorrect and do not prevent the program from functioning. Instead, they indicate weaknesses in design that may slow down development or increase the risk of bugs or failures in the future. Bad code smells can be an indicator of factors that contribute to technical debt. Robert C. Martin calls a list of code smells a "value system" for software craftsmanship.

Often the deeper problem hinted at by a code smell can be uncovered when the code is subjected to a short feedback cycle, where it is refactored in small, controlled steps, and the resulting design is examined to see if there are any further code smells that in turn indicate the need for more refactoring. From the point of view of a programmer charged with performing refactoring, code smells are heuristics to indicate when to refactor, and what specific refactoring techniques to use. Thus, a code smell is a driver for refactoring.

A 2015 study utilizing automated analysis for half a million source code commits and the manual examination of 9,164 commits determined to exhibit "code smells" found that:

- There exists empirical evidence for the consequences of "technical debt", but there exists only anecdotal evidence as to how, when, or why this occurs.
- "Common wisdom suggests that urgent maintenance activities and pressure to deliver features while prioritizing time-to-market over code quality are often the causes of such smells".

<br>
## Referencing controls by string

Comparing control by name, although it works exactly like comparing to a control reference, it has one big downside: when the control no longer exists in the xaml file or has been renamed, the code will still compile and thus the module will not continue to work as expected.

**Bad**
```
if (element.Name == "tbMATPreis")
{
    
}
```

After switching to reference comparison, when the name of *tbMATPreis* changes to e.g. *tbMatPreis*, then the compiler will throw an error, prompting the user to alter the code accordingly.

**Good**
```
if (element == tbMATPreis)
{
    
}
```


<br>
## Referencing columns by index

When referencing columns by index, there is the danger that after some time, the order of the columns will be changed, and the intended column at the given index is no longer valid (we may be referncing a different column altogether or even worse, we might get an *IndexOutOfRangeException*)

**Bad**
```
this.dgMahng.Columns[1].Visible = false;
```

When referencing column by name, we have the guarantee that we are indeed setting the visibility of the control we intend to change

**Good**
```
this.dgtbMahngZeitraum.Visible = false
```