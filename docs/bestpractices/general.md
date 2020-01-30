# General coding style guidelines

## Naming

<br>
**DO** use PascalCasing for class names and method names.

```
public class ClientActivity
{
    public void ClearStatistics()
    {
        //...
    }
    public void CalculateStatistics()
    {
        //...
    }
}
```

<br>
**DO** use camelCasing for method arguments and local variables.

```
public class UserLog
{
    public void Add(LogEvent logEvent)
    {
        int itemCount = logEvent.Items.Count;
        // ...
    }
}
```

<br>
**DO** use PascalCasing for abbreviations 3 characters or more (2 chars are both uppercase)

```
HtmlHelper htmlHelper;
FtpTransfer ftpTransfer;
UIControl uiControl;
```

<br>
**DO** use predefined type names instead of system type names like Int16, Single, UInt64, etc

```
// Correct
string firstName;
int lastIndex;
bool isSaved;
 
// Avoid
String firstName;
Int32 lastIndex;
Boolean isSaved;
```

<br>
**DO** use implicit type var for local variable declarations. Exception: primitive types (int, string, double, etc) use predefined names.

```
var stream = File.Create(path);
var customers = new Dictionary();
 
// Exceptions
int index = 100;
string timeSheet;
bool isCompleted;
```

<br>
**DO** use noun or noun phrases to name a class.

```
public class Employee
{
}
public class BusinessLocation
{
}
public class DocumentCollection
{
}
```

<br>
**DO** prefix interfaces with the letter I.  Interface names are noun (phrases) or adjectives.

```
public interface IShape
{
}
public interface IShapeCollection
{
}
public interface IGroupable
{
}
```

<br>
**DO** name source files according to their main classes. Exception: file names with partial classes reflect their source or purpose, e.g. designer, generated, etc.
```
// Located in Task.cs
public partial class Task
{
    //...
}
```

```
// Located in Task.generated.cs
public partial class Task
{
    //...
}
```

<br>
**DO** organize namespaces with a clearly defined structure
```
// Examples
namespace Company.Product.Module.SubModule
namespace Product.Module.Component
namespace Product.Layer.Module.Group
```

<br>
**DO** vertically align curly brackets.
```
// Correct
class Program
{
    static void Main(string[] args)
    {
    }
}
```

<br>
**DO** declare all member variables at the top of a class, with static variables at the very top.
```
// Correct
public class Account
{
    public static string BankName;
    public static decimal Reserves;
 
    public string Number {get; set;}
    public DateTime DateOpened {get; set;}
    public DateTime DateClosed {get; set;}
    public decimal Balance {get; set;}
 
    // Constructor
    public Account()
    {
        // ...
    }
}
```

<br>
**DO** use singular names for enums. Exception: bit field enums.
```
// Correct
public enum Color
{
    Red,
    Green,
    Blue,
    Yellow,
    Magenta,
    Cyan
}
 
// Exception
[Flags]
public enum Dockings
{
    None = 0,
    Top = 1, 
    Right = 2, 
    Bottom = 4,
    Left = 8
}
```

<br>
**AVOID** using Abbreviations. Exceptions: abbreviations commonly used as names, such as Id, Xml, Ftp, Uri
```
// Correct
UserGroup userGroup;
Assignment employeeAssignment;
 
// Avoid
UserGroup usrGrp;
Assignment empAssignment;
 
// Exceptions
CustomerId customerId;
XmlDocument xmlDocument;
FtpHelper ftpHelper;
UriPart uriPart;
```

<br>
**DO NOT** explicitly specify a type of an enum or values of enums (except bit fields)
```
// Don't
public enum Direction : long
{
    North = 1,
    East = 2,
    South = 3,
    West = 4
}
 
// Correct
public enum Direction
{
    North,
    East,
    South,
    West
}
```

<br>
**DO NOT** suffix enum names with Enum

```
// Don't
public enum CoinEnum
{
    Penny,
    Nickel,
    Dime,
    Quarter,
    Dollar
}
 
// Correct
public enum Coin
{
    Penny,
    Nickel,
    Dime,
    Quarter,
    Dollar
}
```

<br>
**DO NOT** use Underscores in identifiers. Exception: you can prefix private static variables with an underscore.

```
// Correct
public DateTime clientAppointment;
public TimeSpan timeLeft;
 
// Avoid
public DateTime client_Appointment;
public TimeSpan time_Left;
 
// Exception
private DateTime _registrationDate;
```

<br>
## Formatting

- Write only one statement per line.
- Write only one declaration per line.
- If continuation lines are not indented automatically, indent them one tab stop (four spaces).
- Add exactly one blank line between method definitions and property definitions.

```
public string MyProperty { get; set; }

public virtual void MyMethod(string value)
{
    if (value == null) throw new ArgumentNullException(nameof(value));

    var belposRows = tSet.belpos.DefaultViewRows
        .Where(x => x.projekt_id == BelRow.projekt_id && x.GetRowState() != EnumRowState.Deleted);

    foreach (var belposRow in belposRows)
    {
        belposRow.SetRowState(EnumRowState.New);
    }
}

public virtual void AnotherMethod(string projektId, dsBel.belposRow belposRow = null)
{
    if (projektId == null) throw new ArgumentNullException(nameof(projektId));

    if (projektId.IsNotNullOrEmpty())
    {
        var fibuCobjId = Sql.TrySelectValue("select fibu_cobjid from projekte where id = :projekt", new { projekt = projektId }).ToStringNN();
        if (fibuCobjId.IsNotNullOrEmpty())
        {
            if (belposRow == null)
            {
                RetrieveBelegFibuKostenobjekt(BelRow, fibuCobjId);
            }
            else if (belposRow.fibu_cobjid.IsNullOrEmpty())
            {
                RetrieveBelposFibuKostenobjekt(belposRow, fibuCobjId);
            }
        }
    }
}
```

