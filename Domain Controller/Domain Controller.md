# Proposal: Domain Controller Role
## Personas
 * [Sandra Summers - SysAdmin MacGuyver](https://fedoraproject.org/wiki/Server/Personas#Persona_.231:_SysAdmin_MacGuyver)
 * [Andy Grant - Junior Enterprise SysAsmin](https://fedoraproject.org/wiki/Server/Personas#Persona_.234:_Junior_Enterprise_SysAdmin)

## User Stories
### Green-field setup
Sandra Summers works for a small organization using Linux servers and desktops that is just beginning to expand. They have outgrown the use of individually-configured systems and need to start managing configuration centrally. As a cornerstone of this effort, she needs to build a centrally-managed identity and authentication system, which means setting up a domain. She has an extremely tight budget, so the cost of Windows Server licenses may be prohibitive.

Sandra needs her identity management system to ensure that users are identified and authenticated appropriately on all Linux client systems for which they require access and are denied access to any systems that are not required by their job duties.

### Scaling and fault-tolerance
As the organization grows, Sandra hires Andy Grant to help her manage the load. Andy is relatively new to the information technology world. Sandra tasks Andy to deploy a set of replica domain controllers to handle the increase in users and systems as well as to provide redundancy if one or more of the domain controllers become unavailable.

### Integration into an existing environment
Sandra and Andy's company gets acquired by a larger company that has an existing Microsoft Windows domain serving its users. In order to ensure that the transation goes smoothly, Sandra wants to merge their old environment into the new one by having it treated as a new domain in their new company's existing domain forest. This integration must enable users from the new parent company to interact with all of the existing systems in their network.

## Detailed Technical Requirements
(Note: some of these may already exist)
### FreeIPA
 * An installer that can be repeatedly driven by a Ansible playbook without returning an error on any valid configuration.
 * Capability to enroll a machine as a replica of an existing domain.
  * This enrollment may not require preparation steps performed on a separate machine.
  * This enrollment must be possible to initiate solely from the machine requesting the enrollment.
 * Support for Linux client hosts.
 * Must provide appropriate identity-lookup services to properly-configured LDAP clients.
  * Must be capable of serving LDAP requests, including TLS-encrypted LDAP requests, on port 389.
  * Must be capable of serving LDAPS (LDAP encrypted with SSL) requests on port 636.
  * Must be capable of returning LDAP and LDAPS search results using simple auth or SASL/GSSAPI auth.
  * Must be capable of returning POSIX user accounts through the SSSD service on the client.
 * Must provide appropriate authentication services to properly configured clients.
  * Must be capable of performing user authentication against the LDAP server by using an authenticated LDAP bind over an encrypted (LDAP+TLS or LDAPS) channel.
  * Must be capable of performing user authentication against the Kerberos server by using the Kerberos TGT acquisition protocol.
 * Must provide appropriate domain-name services to properly configured DNS clients.
  * Must be capable of serving DNS host records on port 53.
  * Must serve DNS SRV records for ldap and kerberos on port 53
 * Must provide a graphical (web-based) and non-graphical (CLI or API) user environment for creating and managing POSIX users, groups and hosts.
 * Must provide a graphical (web-based) and non-graphical (CLI or API) user environment for managing access-control rules.
 * Capability to enroll a machine as a domain in an existing Active Directory Forest.
  * As far as possible, this should be possible to initiate solely from the machine requesting enrollment. This may require developing PowerShell capabilities to configure the Windows machine.
 * Clients with accounts from a trusted Active Directory domain must be able to log into Linux hosts enrolled in the FreeIPA domain using their Windows credentials for systems on which they are authorized.
 * Long-term: FreeIPA must support trusted FreeIPA domains.

### Cockpit
 * Cockpit must provide a graphical user experience for executing all of the workflows described in this document.
 * Cockpit must be able to export an Ansible playbook at the end of the workflow, prior to executing the changes.
 * Cockpit must be able to import an Ansible playbook for domain creation and execute it. (Expert mode for custom changes made to the Ansible playbook).

## Non-requirements
These are a list of features that will be expressly out of scope for this project.

 * Support for any non-Linux client in the FreeIPA domain.
 
