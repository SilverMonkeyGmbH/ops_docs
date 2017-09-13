=======================
config.json sample file
=======================

.. code-block:: json
    =======================
    config.json sample file
    =======================
    
    .. code-block:: json
        {
          "sites": [
            {
              "id": 1,
              "displayName": "Everything",
              "panelIds": [ 2 ],
              "roleNames": { "values": [ "Admin", "User" ] }
            },
            {
              "id": 2,
              "displayName": "Restricted",
              "panelIds": [ 3 ],
              "roleNames": { "values": [ "Admin", "RoleWithWildCard*" ] }
            }
          ],
          "panels": [
            {
              "id": 2,
              "table": "[dbo].[Item]",
              "permissionTable": "[dbo].[ItemsRoles]",
              "columns": [
                {
                  // Name of the db column for this field.
                  "fieldName": "name",
                  // Name displayed on frontend for this field.
                  "displayName": "Computer Name"
                },
                {
                  // Name of the db column for this field.
                  "fieldName": "description",
                  // Name displayed on frontend for this field.
                  "displayName": "Computer Description"
                },
                {
                  // Name of the db column for this field.
                  "fieldName": "dn",
                  // Name displayed on frontend for this field.
                  "displayName": "dn"
                },
                {
                  // Name of the db column for this field.
                  "fieldName": "domainAlias",
                  // Name displayed on frontend for this field.
                  "displayName": "Alias"
                }
              ],
              "searchField": "name",
              "defaultCondition": "",
              "filterIds": [ 0, 3 ]
            },
            {
              "id": 3,
              "table": "[dbo].[Item]",
              "permissionTable": "[dbo].[ItemsRoles]",
              "columns": [
                {
                  "fieldName": "name",
                  "displayName": "Computer Name"
                },
                {
                  "fieldName": "description",
                  "displayName": "Computer Description"
                },
                {
                  "fieldName": "dn",
                  "displayName": "dn"
                },
                {
                  "fieldName": "domainAlias",
                  "displayName": "Alias"
                }
              ],
              "searchField": "name",
              "defaultCondition": "",
              "filterIds": [ 3 ]
            }
          ],
          "filters": [
            {
              "id": 0,
              "displayName": "All",
              "actionsMenuId": 0
            },
            {
              "id": 3,
              "displayName": "With description 2",
              "condition": "Name IS NOT NULL",
              "actionsMenuId": 7
            }
          ],
          "contextMenus": [
            {
              "itemType": "computer",
              "menuId": 1
            },
            {
              "itemType": "app",
              "menuId": 3
            }
          ],
          "dndMenus": [
            {
              "itemTypes": [ "computer", "app" ],
              "menuId": 4
            },
            {
              "itemTypes": [ "computer", "appPrd" ],
              "menuId": 9
            }
          ],
          "menus": [
            {
              "id": 0,
              "name": "A S1 P1",
              "menuItems": [
                {
                  "displayName": "Add computer",
                  "urlTemplate": "http: //v6.com/add_computer"
                }
              ]
            },
            {
              "id": 1,
              "name": "C S1 P1",
              "menuItems": [
                {
                  "displayName": "Delete computer",
                  "urlTemplate": "http: //v6.com/delete_computer/:id",
                  "roleNames": { "values": [ "RoleWithWildCard*", "Admin" ] }
                },
                {
                  "displayName": "Edit computer",
                  "urlTemplate": "http: //v6.com/edit_computer/:id"
                }
              ]
            }
          ]
        }
