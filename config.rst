Root object definition
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"ConnectionString","string","The database that will be used to query Roles","required"
	"Sites","array<Site>","The different Sites that contain the Panels","required"
	"Menues","array<Menu>","Menues contain Actions (MenuItems) that can be invoked by users. Menus can be displayed in different flavors: as an ActionMenu, ContextMenu, DragAndDropMenu...",""



Site object definition
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"DisplayName","string","","required"


Menu object definition
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10

	"Items","array<MenuItem>","",""


MenuItem object definition
======================
.. csv-table::
   :header: "Name","Type","Description","Required"
   :widths: 10,10,10,10



