# Introduction

## Module

Each „complete” module has:

- a Window Handling Object **WHO:**  specifies the behavior of the controls
- a BusinessObject **busObj:** data manipulation; direct access to the dataSet (and dataSet fields)
- at least one **DataSet**

A **Window Handling Object** defines the behavior of the window itself and of the controls within it. It is the place where the „call-to-action” happens, i.e. it can respond to event handlers of any type. It responds to various events triggered by the window or by the controls, it holds references to the controls and can modify their properties at any given time. It does not contain business logic functionality; it delegates the functionality to the Business Object. It is the component that is able to handle exceptions and decide how the exception is handled (show message to user, retry, fail silently, etc.)

A **Business Object** is the part of the program that encodes the real-world [business rules](https://en.wikipedia.org/wiki/Business_rule "Business rule") that determine how data can be [created, stored, and changed](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete "Create, read, update and delete"). It is contrasted with the remainder of the software that might be concerned with lower-level details of managing a [database](https://en.wikipedia.org/wiki/Database "Database"). It is an executor of commands usually triggered by a Window Handling Object or a parent Business Object.

It should not implement events of any type; the responsibility of „call-to-action” belongs to the Window Handling Object.

It does not reference any visual components (WPF); it does not display user-level information.

When an unexpected result occurs inside of a function, the best practice would be to throw Exception instead of returning error-value.

It should not handle Exceptions in try/catch blocks; in the catch blocks, it should always call „throw;” after some action is performed such as Logging the error.

Uses LoggerSink sparingly (best practice: not at all).

**Note****:** the code-examples used in section **BusinessObject** and **Window Handling Object** are code sequences from Production Feedback-Module (shortcut: **PRM**)

![diagram](https://tanghel.github.io/images/1.introduction.01.png)

## DataSet Definition

A DataSet is a data container composed of tables (DataTables) that contain rows (DataRows), uses SQL queries to retrieve that data from the database, tracks changes to each columns and generated update/insert/delete statements transparently when required to write data back into the database.
Each DataRow may have one of the following RowStates:

- **New**: the row was added to the dataSet and will be ignored on Save
- **EditingNew**: the row was already edited and it’s prepared to be saved
- **Modified**: an existing row was modified
- **NotModified**: an existing row was retrieved from the db
- **Deleted**: the row was marked as deleted, will be deleted only at Save
- **None**: the row was not added to the collection; the row is detached


For updateable DataSets, the tables must be arranged in the same order, in which the primary-key inserts are done.
For the Delete operation, the DataSet will do the action in the reverse order.

## Window Handling Object

Never call Override-Methods, because:

- these methods are in general called automatically from the framework, as a result of an action
- they are usually part of a sequence of actions (OnSave() is called after OnPreSave() – if the latter returned>0 – and if OnSave() returns>0, OnPostSave() is called)
- these methods are the equivalent of "event handlers", which should never be called directly; if the code sequence contained in the override method is needed, a common method should be written and called every time it is needed
- whenever an event has to be called, it means that the functionality behind the event should be extracted into a method; in this case, the method can be called from the event itself, as well as anywhere else, explicitly. 

**Example**: 

- call WHO-method in override Method:

```
public override void OnNew(UIElement sourceControl)
{
    if (sourceControl == dgMaterial)
    {
        NewMaterial();
    }
}
```

- call BusinessObject-method from WHO-method:
```
public virtual void NewMaterial()
{
    var material = BusObj.NewMatRow();
    if (material == null) return;
}

```

Order of execution: Event -> WHO-method -> BusObj. 

Do not call your BusinessObject-Method in a WHO override method. 

Do not write Business-Logic inside WHO methods.