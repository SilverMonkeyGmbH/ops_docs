=============
Config schema
=============


This document describes the schema of the config.json file. The config.json file is used to configure the available views and actions for the web-app.


Root object
==================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"Sites","array<SiteConfig>","A list of Sites","required"
	"Panels","array<PanelConfig>","A list of Panels","required"
	"Filters","array<FilterConfig>","A list of Filters","required"
	"ContextMenus","array<ContextMenu>","A list of ContextMenus","required"
	"DndMenus","array<DnDMenu>","A list of DndMenus","required"
	"Menus","array<Menu>","A list of Menus","required"



SiteConfig
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"Id","integer","","required"
	"DisplayName","string","The name that will be displayed to users","required"
	"PanelIds","array<integer>","A Site can display several Panels that are specified here","required"
	"RoleNames","RoleNames","A Site can be shown to only authorized users, which can be described here",""


RoleNames
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"Values","array<string>","The actual values. Roles can end with a wildcard, to match more than one role at once. The symbol * (asterisk) is used. Example: Admin* would match any role that begins with **Admin**, so Admin, AdminHamburg and AdminBerlin would match the rule. GlobalAdmin however would not match.","required"


PanelConfig
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"Id","integer","The id property","required"
	"SearchField","string","The property name (usually the name of the column) that should be used for searching","required"
	"Columns","array<Column>","The columns that should be displayed in the table. Don't forget that every item should have the properties **id** and **itemType** even if they are not displayed","required"
	"FilterIds","array<integer>","Specifies the available Filters","required"
	"Table","string","The name of the table to display","required"
	"PermissionTable","string","The many-to-many intermediate table between the table specified in the Table property and the Role table","required"
	"DefaultCondition","string","A sql expression to filter the items",""


Column
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"FieldName","string","The name of the property (usually a database column)","required"
	"DisplayName","string","The label that should be displayed in the UI","required"


FilterConfig
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"Id","integer","Id must be unique among all filters","required"
	"DisplayName","string","The name that will be displayed in the UI","required"
	"ActionsMenuId","integer","Every filter is bound to a specific ActionMenu","required"
	"RoleNames","RoleNames","A filter can be made available to specific roles. If this property is not set, the filter will be available for all users",""
	"Condition","string","An SQL condition that is used as part of a where clause when querying the database table",""


ContextMenu
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"ItemType","string","TODO","required"
	"MenuId","integer","The id of the corresponding Menu","required"


DnDMenu
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"ItemTypes","array<string>","A combination (a list) of itemtypes, for which this Drag-and-Drop-Menu will be available","required"
	"MenuId","integer","The id of the corresponding Menu","required"


Menu
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"Id","integer","","required"
	"Name","string","","required"
	"MenuItems","array<MenuItem>","A list of actions that are bound to this menu","required"


MenuItem
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"DisplayName","string","Will be used in the UI","required"
	"UrlTemplate","string","UrlTemplate is used to create a url at runtime with specified parameters from items. Parameters are extracted from the items contextual to the menu. They should have this format: **{[itemType].[column]}** where **itemType** is the mandatory item type that all items should have as a property. Example: **https://v6.com/install?idapp={app.id}&idcomp={computer.id}**.","required"
	"RoleNames","RoleNames","A MenuItem can be restricted to users that belong to certain Roles",""


