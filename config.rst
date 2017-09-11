Root object definition
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"Sites","array<SiteConfig>","A list of Sites","required"
	"Panels","array<PanelConfig>","A list of Panels","required"
	"Filters","array<FilterConfig>","A list of Filters","required"
	"ContextMenus","array<ContextMenu>","A list of ContextMenus","required"
	"DndMenus","array<DnDMenu>","A list of DndMenus","required"
	"Menus","array<Menu>","A list of Menus","required"



SiteConfig object definition
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"Id","integer","","required"
	"DisplayName","string","","required"
	"PanelIds","array<>","","required"
	"RoleNames","","",""


RoleNames object definition
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"Values","array<>","",""


PanelConfig object definition
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"Id","integer","","required"
	"SearchField","string","","required"
	"Columns","array<Column>","","required"
	"FilterIds","array<>","","required"
	"Table","string","","required"
	"PermissionTable","string","","required"
	"DefaultCondition","null","",""


Column object definition
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"FieldName","string","The name of the property (usually a database column)","required"
	"DisplayName","string","The label that should be displayed in the UI","required"


FilterConfig object definition
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"Id","integer","Id must be unique among all filters","required"
	"DisplayName","string","The name that will be displayed in the UI","required"
	"ActionsMenuId","integer","Every filter is bound to a specific ActionMenu","required"
	"RoleNames","","A filter can be made available to specific roles. If this property is not set, the filter will be available for all users",""
	"Condition","null","An SQL condition that is used as part of a where clause when querying the database table",""


ContextMenu object definition
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"ItemType","string","TODO","required"
	"MenuId","integer","The id of the corresponding Menu","required"


DnDMenu object definition
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"ItemTypes","array<>","A combination (a list) of itemtypes, for which this Drag-and-Drop-Menu will be available","required"
	"MenuId","integer","The id of the corresponding Menu","required"


Menu object definition
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"Id","integer","","required"
	"Name","string","","required"
	"MenuItems","array<MenuItem>","A list of actions that are bound to this menu","required"


MenuItem object definition
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"DisplayName","string","Will be used in the UI","required"
	"UrlTemplate","string","UrlTemplate is used to create a url at runtime with specified parameters. ++ explanation of parameters ++","required"
	"RoleNames","","A MenuItem can be restricted to users that belong to certain Roles",""


