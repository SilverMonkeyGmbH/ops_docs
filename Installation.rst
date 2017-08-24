=============
Installation
=============

.. contents:: `In this article:`
    :depth: 2
    :local:



ops-auth
--------

The ops-auth module (or simpler just auth module) is a service to retrieve OPS user roles (not Windows or Azure AD roles).

.. warning:: Note.
   The ops-auth module will be replaced in the near future


Requirements
^^^^^^^^^^^^

================================== ============================================
Name                               Version
================================== ============================================
Operating System                   Windows 7 or Windows Server 2012 (or higher)
Webserver                          IIS 7 (or higher)
.NET Framework:                    4.5.2 (or higher)
================================== ============================================


Installation
^^^^^^^^^^^^

The module needs to be installed as an IIS application for a website. The websites url needs to be known by SIM before compiling the application.

======================================= ===================================
Setting                                 Value
======================================= ===================================
Applicationname                         auth
Applicationpool .NET CLR Version        v4.0.30319
Applicationpool Managed pipeline mode   Integrated
Authentication                          Only Windows Authentication enabled
======================================= ===================================


Configuration (Web.config)
^^^^^^^^^^^^^^^^^^^^^^^^^^

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


ops-api
-------

The ops-api module is a services that provides access to one or more datastores and configuration of views and actions for clients (for example the ops-webapp). Access to the data, the views and actions is determined by SIM/OPS roles. Access control for the views and actions is defined in a configuration file. Access control for the data is defined in the database.


Requirements
^^^^^^^^^^^^

================================== ============================================
Name                               Version
================================== ============================================
Operating System                   Windows 7 or Windows Server 2012 (or higher)
Webserver                          IIS 7 (or higher)
.NET Framework:                    4.5.2 (or higher)
================================== ============================================


Installation
^^^^^^^^^^^^

The module needs to be installed as an IIS application for a website. The websites url needs to be known by SIM before compiling the application.


+---------------------------------------+-----------------------------------------------+
|Applicationname                        |ops-api                                        |
+---------------------------------------+-----------------------------------------------+
|                |.NET CLR Version      |No Managed Code                                |
|                +----------------------+-----------------------------------------------+
|Applicationpool |Managed pipeline mode |Integrated                                     |
|                +----------------------+-----------------------------------------------+
|                |Identity              |Custom account with read access to the database|
+----------------+----------------------+-----------------------------------------------+
|Authentication                         |Only anonymous authentication enabled          |
+---------------------------------------+-----------------------------------------------+


IIS Modules
^^^^^^^^^^^

The AspNetCoreModule module needs to be activated for this module.


Database setup
^^^^^^^^^^^^^^

