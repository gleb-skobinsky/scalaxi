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

1) AddItem
  
3) ChangePageAsync, ChangePageByName, ChangePageByNameAction, Dispose, EditItem, ExecuteDataflow, ExecuteScript, ExecuteWorkflow, NavigationBack, OnAddItemCommand, OnChangePageCommand, OnComponentOpenCommand, OnEditItemCommand, OnExecuteDataflowCommand, OnExecuteScriptCommand, OnExecuteWorkflowCommand, OnNavigationBackCommand, OpenComponent


Module <code>Scalaxi.Platform.Shared.RenderEngine.Models.Commands</code> incorporates the following classes for instanciating commands:

1. AddItemCommand: accepts an argument of type <code>System.Guid</code> to add an item to the context. Commands of this class are accepted by method <code>context.Commands.AddItem</code>. <b>The nature and behaviour of the added "item" is to be clarified.</b>
2. ChangePageCommand
3. EditItemCommand
4. ExecuteDataflowCommand
5. ExecuteScriptCommand
6. ExecuteWorkflowCommand
7. OpenComponentCommand






