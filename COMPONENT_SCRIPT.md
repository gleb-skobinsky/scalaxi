The uniform class <code>context</code> contains the following attributes:

```
Commands, 
ConfirmationService, 
DataModel, 
ExecuteDataflow, 
ExtendedData, 
Form, 
Logger, 
Model, 
PlatformServices, 
Properties, 
Runtime, 
SessionManager,
Subscriptions, 
UserInfo, 
Workflows
```

1. Module "Commands"

This module is used to launch various script-external actions to manipulate database connection, component/page redirection, corresponding events etc.

* AddItem
  
* ChangePageAsync

* ChangePageByName: accepts an argument of type <code>str</code>. Redirects to another page of the same component the user is currently in.

* ChangePageByNameAction

* Dispose

* EditItem

* ExecuteDataflow

* ExecuteScript

* ExecuteWorkflow

* NavigationBack: accepts no arguments. Redirects to previous page.

* OnAddItemCommand

* OnChangePageCommand

* OnComponentOpenCommand

* OnEditItemCommand

* OnExecuteDataflowCommand

* OnExecuteScriptCommand

* OnExecuteWorkflowCommand

* OnNavigationBackCommand

* OpenComponent

- Command types

Module <code>Scalaxi.Platform.Shared.RenderEngine.Models.Commands</code> incorporates the following classes for instantiating commands:

1. AddItemCommand: accepts an argument of type <code>System.Guid</code> to add an item to the context. Commands of this class are accepted by method <code>context.Commands.AddItem</code>. <b>The nature and behaviour of the added "item" is to be clarified.</b>
2. ChangePageCommand
3. EditItemCommand
4. ExecuteDataflowCommand
5. ExecuteScriptCommand
6. ExecuteWorkflowCommand
7. OpenComponentCommand: accepts three arguments: 1) Type: <code>System.Guid</code>; description: guid of component in the database (the same one as displayed in the url). 2) Type: <code>System.Guid</code>; description: guid of the page which will be opened upon component initialization. If <code>None</code>, the main page of the component will be opened. 3) Type: <code>"System.Collections.Dictionary[str,str]()"</code>. A dictionary of arguments to be passed from the "old" component to the "new" one.

3. Module ConfirmationService
4. Module DataModel

DataModel is a container for the component model with all its fields. It changes dynamically as the user provides some input and can be manipulated directly from the script.

For example:
```
datamodel = context.DataModel.Model
def change_username:
    datamodel.Username = "some-user"
```



