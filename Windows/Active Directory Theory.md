# Active Directory Theory
What is Active Directory? - 

Active Directory is a collection of machines and servers connected inside of domains, that are a collective part of a bigger forest of domains, that make up the Active Directory network. Active Directory contains many functioning bits and pieces, a majority of which we will be covering in the upcoming tasks. To outline what we'll be covering take a look over this list of Active Directory components and become familiar with the various pieces of Active Directory: 

*   Domain Controllers
*   Forests, Trees, Domains
*   Users + Groups 
*   Trusts
*   Policies 
*   Domain Services

**Domain Controllers -**
------------------------

﻿A domain controller is a Windows server that has Active Directory Domain Services (AD DS) installed and has been promoted to a domain controller in the forest. Domain controllers are the center of Active Directory -- they control the rest of the domain. I will outline the tasks of a domain controller below: 

*   holds the AD DS data store 
*   handles authentication and authorization services 
*   replicate updates from other domain controllers in the forest
*   Allows admin access to manage domain resources

What database does the AD DS contain?

NTDS.dit

Where is the NTDS.dit stored?

%SystemRoot%\\NTDS

**Forest Overview -**
---------------------

﻿﻿A forest is a collection of one or more domain trees inside of an Active Directory network. It is what categorizes the parts of the network as a whole.

The Forest consists of these parts which we will go into farther detail with later:

*   Trees - A hierarchy of domains in Active Directory Domain Services
*   Domains - Used to group and manage objects 
*   Organizational Units (OUs) - Containers for groups, computers, users, printers and other OUs
*   Trusts - Allows users to access resources in other domains
*   Objects - users, groups, printers, computers, shares
*   Domain Services - DNS Server, LLMNR, IPv6
*   Domain Schema - Rules for object creation

The four types of users are: 
-----------------------------

*   Domain Admins - This is the big boss: they control the domains and are the only ones with access to the domain controller.
*   Service Accounts (Can be Domain Admins) - These are for the most part never used except for service maintenance, they are required by Windows for services such as SQL to pair a service with a service account
*   Local Administrators - These users can make changes to local machines as an administrator and may even be able to control other normal users, but they cannot access the domain controller
*   Domain Users - These are your everyday users. They can log in on the machines they have the authorization to access and may have local administrator rights to machines depending on the organization.