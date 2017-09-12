=============
Installation
=============

.. contents:: `In this article:`
    :depth: 2
    :local:


--------
ops-auth
--------


The module needs to be installed as an IIS application for a website. The websites url needs to be known by SIM before compiling the application.

+-----------------------------------------+-------------------------------------------------+
| Applicationname                         | auth                                            |
+-----------------------------------------+-------------------------------------------------+
| Applicationpool | .NET CLR Version      | v4.0.30319                                      |
|                 +-----------------------+-------------------------------------------------+
| Applicationpool | Managed pipeline mode | Integrated                                      |
|                 +-----------------------+-------------------------------------------------+
| Applicationpool | Identity              | Custom account with read access to the database |
+-----------------+-----------------------+-------------------------------------------------+
| Authentication                          | Only anonymous authentication enabled           |
+-----------------------------------------+-------------------------------------------------+


-------
ops-api
-------

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

The AspNetCoreModule module needs to be activated for this application.


--------------------
ops-webapp / ops-web
--------------------

The ops-webapp can be hosted in any webserver.
If it is hosted in IIS the following settings apply:

+---------------------------------------+-----------------------------------------------+
|Applicationname                        |ops or ops-web or ops-webapp                   |
+---------------------------------------+-----------------------------------------------+
|                |.NET CLR Version      |v4.0.30319                                     |
|                +----------------------+-----------------------------------------------+
|Applicationpool |Managed pipeline mode |Integrated                                     |
|                +----------------------+-----------------------------------------------+
|                |Identity              |Applicationpool Identity                       |
+----------------+----------------------+-----------------------------------------------+
|Authentication                         |Only anonymous authentication enabled          |
+---------------------------------------+-----------------------------------------------+
