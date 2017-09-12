=====
Setup
=====

.. contents:: `In this article:`
    :depth: 2
    :local:


--------
ops-auth
--------

The module requires an MS SQL Server and database that provides the mapping between Windows domain roles and OPS roles. The connection to the database can be specified in the modules Web.config DefaultConnectionString node. The connection strings property "integrated security" SHOULD have the value "true", the "provider name" property SHOULD have the value "System.Data.EntityClient".
Under the node appSettings the value of "DomainName" MUST have the name of the windows domain.

example Web.config

.. code-block:: xml

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
        <appSettings>
            <add key="DomainName" value="phatconsulting.group" />
        </appSettings>
        <connectionStrings>
            <add name="DefaultConnectionString" connectionString="data source=simsrv042;initial catalog=SIM_OPS_R042;integrated security=True;MultipleActiveResultSets=True;" providerName="System.Data.EntityClient" />
        </connectionStrings>
        <system.web>
            <authentication mode="Windows" />
            <compilation targetFramework="4.6.1">
            <assemblies>
                <add assembly="System.Security, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B03F5F7F11D50A3A" />
                <add assembly="System.DirectoryServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B03F5F7F11D50A3A" />
                <add assembly="System.DirectoryServices.AccountManagement, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />
            </assemblies>
            </compilation>
            <httpRuntime targetFramework="4.5.2" />
        </system.web>
    </configuration>
    <!--ProjectGuid: b03c2d11-e5ac-4242-a5c2-862a3787e00a-->

Database
^^^^^^^^

The module expects a Table named "Role_Group" with columns "RoleId" (uniqueidentifier, not null) and "GroupName" (varchar, not null) in the given database. The Groupname is the name of a windows domain group. The RoleId is the id of a SIM/OPS role. The corresponding Role table is not used by the auth module and therefore CAN be absent.


-------
ops-api
-------


Database
^^^^^^^^

The module expects following tables and relationships:


**Role** table:

====== ===============================
Column Type
====== ===============================
Id     PK, uniqueidentifier, not null
Name   Name, varchar(1000), not null
====== ===============================


any number of **Item** tables: (name can be chosen arbitrarily)

======== ===============================
Column   Type
======== ===============================
Id       PK, uniqueidentifier, not null
ItemType varchar(15), not null
======== ===============================


foreach **Item** table there MUST be exactly one corresponding **Item_Role** table (name can be chosen arbitrarily), that defines a many-to-many relationship between the corresponding **Item** table and the **Role** table:

======== ===========================================
Column   Type
======== ===========================================
RoleId   FK Role(Id), uniqueidentifier, not null
ItemId   FK **Item**(Id), uniqueidentifier, not null
======== ===========================================

.. note:: database conventions
    SIM (usually) uses 
    - singular for table names (for example "Application" instead of "Applications")
    - "Id" as the name for the PRIMARY KEY
    - The GUID/uniqueidentifier type for the PRIMARY KEY column
    - The names of the involved tables seperated by an underscore in a many to many relationship (for example "Computer_Role")
    - Tablename + "Id" for FOREIGN KEYS (for example "RoleId")




