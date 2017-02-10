# Quick fix for the UI5 component sap.m.Tree
The sap.m.Tree component (UI5 version 1.42.9) throws an exception on expansion.  This behaviour seems to be as a result of the code using the JavaScript max integer value as the odata $top parameter

```
aContexts = oBinding.getContexts(0, Number.MAX_SAFE_INTEGER);
```
![alt text](https://answers.sap.com/storage/attachments/18835-ui5-tree-err2.png")

## Fix
Create a new sap.m.Tree component by extending the sap.m.Tree control and overriding the update function with

```
aContexts = oBinding.getContexts(0, 100);
```
And now the tree will expand as expected.

![alt text](https://answers.sap.com/storage/attachments/18836-ui5-tree-err3.png")

## Deploy
You should be able to deploy the UI5 application by importing it into WebIDE. 

## OData service
You can follow this SCN Blog [SCN Blog](https://blogs.sap.com/2015/10/23/treetable-odata-binding/) to create a hierarchy using annotations.
