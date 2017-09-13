============
Introduction
============

.. contents:: `In this article:`
    :depth: 2
    :local:



OPS Module overview
===================

The OPS (Operations) Module enables users to view the current state of different domain entities (such as Computers, Applications, Users etc.) and allows to invoke actions (such as WakeOnLan, Install Application etc.) on these entities.

Access to OPS is controled by the SIM access control system (domain groups are mapped to SIM roles).


The OPS Module consists of three seperate services: ops-auth, ops-api and ops-web. The end-user will only deal with ops-web (the frontend), whereas administrators also need to configure ops-auth and ops-api (the backend).
The OPS Module actions that can be invoked for the domain entities are delegated to v5/v6 Forms. Therefore the OPS Module has a dependency on v5/v6.



ops-auth
--------

The ops-auth module (or simpler just auth module) is a service to retrieve OPS user roles (not Windows or Azure AD roles).

.. warning:: Note.
   The ops-auth module will be replaced in the near future



ops-api
-------

The ops-api module is a service that provides access to one or more sql tables as well as defines the views and actions that will be shown in its clients (for example the ops-web).
Access to the data, the views and actions is determined by SIM roles.



ops-web
--------------------

ops-web is the frontend that end-users will use to view entities and invoke actions on them. The views and actions that are available are configured in ops-api.

