---
title: "MODx.grid.Grid"
_old_id: "1080"
_old_uri: "2.x/developing-in-modx/advanced-development/custom-manager-pages/modext/modx.grid.grid"
---

- [MODx.grid.Grid](#MODx.grid.Grid-MODx.grid.Grid)
- [MODExt-Specific Parameters](#MODx.grid.Grid-MODExtSpecificParameters)
- [Custom Events](#MODx.grid.Grid-CustomEvents)
- [Other Unique Functions](#MODx.grid.Grid-OtherUniqueFunctions)
  - [Custom Store Exception Messages](#MODx.grid.Grid-CustomStoreExceptionMessages)
  - [loadWindow](#MODx.grid.Grid-loadWindow)
  - [remove](#MODx.grid.Grid-remove)
  - [confirm](#MODx.grid.Grid-confirm)
  - [refresh](#MODx.grid.Grid-refresh)
  - [encodeModified](#MODx.grid.Grid-encodeModified)
  - [encode](#MODx.grid.Grid-encode)
- [See Also](#MODx.grid.Grid-SeeAlso)



## MODx.grid.Grid

**Extends:** Ext.grid.EditorGridPanel 
**Key Features:** Connector functionality; easily integrate toolbar items and MODx.Window; built-in context menu functionality.

When instantiating this into a tabbed interface, it's recommended to set preventRender: true in its config to prevent JS rendering issues.

![](/download/attachments/18678079/grid.png?version=1&modificationDate=1302187849000)

MODExt Grids are used to display tabular data, complete with a ColumnModel, top toolbar (tbar) and bottom toolbar (bbar). It has built-in support for paging as well. Grids are populated remotely from a connector request returning a JSON object. Displaying a right-click context menu for each row can easily be achieved by including a "menu" key for each data row in your processor:

``` php 
foreach( $items as $item ) {
    $data[] = array(
        'id'    => $obj->get( 'id' ),
        'name'  => $obj->get( 'name' ),
        'menu'  => array(
            array(
                'text'      => $modx->lexicon( 'my_lexicon' ),
                'handler'   => 'this.myHandler'
            )
        )
    );
}
```

The above code would create a context menu for each item with the text being the lexicon key matching "my\_lexicon," and the handler being the myHandler function registered to your Grid object.

Menus may alternatively (and preferably) be created by extending your JS Grid and adding a "getMenu" method:

``` php 
getMenu: function() {
    var m = [];
    m.push({
        text: _('my_lexicon_key')
        ,handler: this.myHandler
    });
    return m;
}
```

Returning an array of items in the getMenu method will automatically add the items to the context menu.

Revolution 2.0.x grids cannot simply return the array - they will need to call "this.addContextMenuItem(m);" before the end of the function. Returning the array was added in 2.1.

## MODExt-Specific Parameters

First off, MODx.grid.Grid pulls its data remotely, via the "url" config parameter. It loads the baseParams into the call as well, which defaults to:

``` php 
baseParams: { action: 'getList' }
```

You can override the baseParams in your config parameter.

MODx.grid.Grid adds a few unique parameters not found in typical Ext.grid.Grid objects:

| Name | Description | Default |
|------|-------------|---------|
| url | The URL of the connector to load this grid from. |  |
| paging | If true, will enable paging and add the PagingToolbar automatically to the bottom of the grid. | true |
| pageSize | The number of items to page by, if paging == true. Defaults to the System Setting of "default\_per\_page", which is 20. | 20 |
| pageStart | The index to start the paging on. | 0 |
| showPerPage | Whether or not to show the "Per Page" textbox. Defaults to true. | true |
| pagingItems | Any items to add to the right of the "Per Page" textbox on the paging toolbar. Useful for adding extra buttons. | \[\] |
| grouping | If true, will automatically enable grouping on this grid. | false |
| groupBy | The column to group by. Note that the column must be in the column model. | name |
| pluralText | The text for a plural amount of items in the grouped column, ie: "Rows" | Records |
| singleText | The text for a single amount of items in the grouped column, ie: "Row" | Record |
| sortBy | The default column to sort by when grouping and remoteSort are true. | id |
| sortDir | The default column to sort by when grouping and remoteSort are true. | ASC |
| preventRender | Prevent the grid from rendering. Useful when putting the grid in panels or tabs. | 1 |
| autosave | If true, will automatically fire the 'updateFromGrid' processor (or the processor in the saveUrl config param) for this connector when doing in-line editing in the grid. | false |
| saveUrl | The connector URL to call when inline-editing with autosave on. | The value of config.url |
| save\_action | The processor action to call when inline-editing with autosave on. | updateFromGrid |
| saveParams | A JS object of parameters to also send to the saveUrl when auto-saving or when using MODx.grid.Grid's remove method. | {} |
| save\_callback | After auto-saving, run this method. | null |
| preventSaveRefresh | If autosave is true, after saving, will prevent the grid from refreshing. Makes for a more seamless editing experience. | 1 |
| primaryKey | If your grid items have a primary key that's not ID, set it here. | id |
| storeId | A custom ID to give the store for this grid. Will default to a unique Ext ID. | Ext.id() |

For a complete list of all parameters not listed here for grids, see the [ExtJS](http://sencha.com) documentation.

## Custom Events

MODx.grid.Grid adds a few extra events not found in Ext.grid.Grid objects:

| Name | Description |
|------|-------------|
| beforeRemoveRow | Fires before a row is removed when calling the remove() method on the grid (usually done in a context menu) |
| afterRemoveRow | Fires after a row is removed when calling the remove() method on the grid (usually done in a context menu) |
| afterAutoSave | Fires after an inline-edit save is done, if autosave is set to true. |

## Other Unique Functions

MODExt grids come with quite a few other features.

#### Custom Store Exception Messages

If the JSON returned is not a valid data store collection, and contains a "message" parameter, this will be set to the emptyText for the grid and displayed as the first row of the grid. A common usage is to use $modx->error->failure('Message here') in your processors.

#### loadWindow

Automatically load and show a window of any given xtype:

``` php 
grid.loadWindow({
  xtype: 'my-xtype-for-the-window'
  ,blankValues: true /* blanks the values of the window, good for New Object windows, set false for Update windows */
});
```

This will, if blankValues is not set to true, automatically pass in the currently selected row's data into the Window as well, setting its values in the form (assuming your window extends [MODx.Window](developing-in-modx/advanced-development/custom-manager-pages/modext/modx.window "MODx.Window").)

#### remove

MODx.grid.Grid comes with a custom method named 'remove', which automatically fires an AJAX request to your connector set in config.url with the action of "remove", and the ID (or primaryKey set in the config) of the currently selected row. This is useful for context menus.

The method takes one parameter - text - which is the text to display in the confirm dialog that prompts the user if they want to remove the row before actually doing so. The beforeRemoveRow event is fired before the confirm dialog is loaded.

``` php 
grid.remove("Are you sure you want to remove this Item?");
```

#### confirm

The confirm method is a custom method that allows you to pop up a confirmation dialog before executing an action:

``` php 
grid.confirm("approve","Are you sure you want to approve this article?");
```

Similar to remove, it will take the ID/primaryKey of the currently selected row, and send it through to the processor action specified in the first parameter to the confirm method. Once finished, it will refresh the grid.

#### refresh

A custom method that will refresh the grid whenever fired.

#### encodeModified

This will return a JSON object of all modified (dirty) rows and fields. Useful if autosave is set to false.

#### encode

This will return a JSON object of all rows.

## See Also

1. [MODExt MODx Object](developing-in-modx/advanced-development/custom-manager-pages/modext/modext-modx-object)
2. [MODExt Tutorials](developing-in-modx/advanced-development/custom-manager-pages/modext/modext-tutorials)
  1. [1. Ext JS Tutorial - Message Boxes](developing-in-modx/advanced-development/custom-manager-pages/modext/modext-tutorials/1.-ext-js-tutorial-message-boxes)
  2. [2. Ext JS Tutorial - Ajax Include](developing-in-modx/advanced-development/custom-manager-pages/modext/modext-tutorials/2.-ext-js-tutorial-ajax-include)
  3. [3. Ext JS Tutorial - Animation](developing-in-modx/advanced-development/custom-manager-pages/modext/modext-tutorials/3.-ext-js-tutorial-animation)
  4. [4. Ext JS Tutorial - Manipulating Nodes](developing-in-modx/advanced-development/custom-manager-pages/modext/modext-tutorials/4.-ext-js-tutorial-manipulating-nodes)
  5. [5. Ext JS Tutorial - Panels](developing-in-modx/advanced-development/custom-manager-pages/modext/modext-tutorials/5.-ext-js-tutorial-panels)
  6. [7. Ext JS Tutoral - Advanced Grid](developing-in-modx/advanced-development/custom-manager-pages/modext/modext-tutorials/7.-ext-js-tutoral-advanced-grid)
  7. [8. Ext JS Tutorial - Inside a CMP](developing-in-modx/advanced-development/custom-manager-pages/modext/modext-tutorials/8.-ext-js-tutorial-inside-a-cmp)
3. [MODx.combo.ComboBox](developing-in-modx/advanced-development/custom-manager-pages/modext/modx.combo.combobox)
4. [MODx.Console](developing-in-modx/advanced-development/custom-manager-pages/modext/modx.console)
5. [MODx.FormPanel](developing-in-modx/advanced-development/custom-manager-pages/modext/modx.formpanel)
6. [MODx.grid.Grid](developing-in-modx/advanced-development/custom-manager-pages/modext/modx.grid.grid)
7. [MODx.grid.LocalGrid](developing-in-modx/advanced-development/custom-manager-pages/modext/modx.grid.localgrid)
8. [MODx.msg](developing-in-modx/advanced-development/custom-manager-pages/modext/modx.msg)
9. [MODx.tree.Tree](developing-in-modx/advanced-development/custom-manager-pages/modext/modx.tree.tree)
10. [MODx.Window](developing-in-modx/advanced-development/custom-manager-pages/modext/modx.window)