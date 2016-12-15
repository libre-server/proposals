# Proposal: Domain Controller Role
## Personas
 * [Sandra Summers - SysAdmin MacGuyver](https://fedoraproject.org/wiki/Server/Personas#Persona_.231:_SysAdmin_MacGuyver)
 * [Andy Grant - Junior Enterprise SysAsmin](https://fedoraproject.org/wiki/Server/Personas#Persona_.234:_Junior_Enterprise_SysAdmin)

## User Stories
### Green-field setup
Sandra Summers works for a small organization using Linux that is just beginning to expand. They have outgrown the use of individually-configured systems and need to start managing configuration centrally. As a cornerstone of this effort, she needs to build a centrally-managed identity and authentication system, which means setting up a domain. She has an extremely tight budget, so the cost of Windows Server licenses may be prohibitive.

Sandra needs her identity management system to ensure that users are identified and authenticated appropriately on all systems for which they require access and are denied access to any systems that are not required by their job duties.

### Scaling and fault-tolerance
As the organization grows, Sandra hires Andy Grant to help her manage the load. Andy is relatively new to the information technology world. Sandra tasks Andy to deploy a set of replica domain controllers to handle the increase in users and systems as well as to provide redundancy if one or more of the domain controllers become unavailable.

### Integration into an existing environment
Sandra and Andy's company gets acquired by a larger company that has an existing Microsoft Windows domain serving its users. In order to ensure that the transation goes smoothly, Sandra wants to merge their old environment into the new one by having it treated as a new domain in their new company's existing domain forest. This integration must enable users from the new parent company to interact with all of the existing systems in their network.

## Milestones
### Proof-of-concept (no public deliverable)
 * The administrative user must be able to install FreeIPA as the sole domain in a new forest
 * The administrative user must be able to perform the installation using a graphical tool as part of the Cockpit admin console.
 * The administrative user must be provided with an Ansible playbook allowing them to reproduce (or modify) the behavior that the GUI console would perform.
 * The administrative user must be able to execute the Ansible playbook independent of Cockpit.
 
### Minimum Viable Project (Fedora 27, late 2017)
 * In addition to the PoC capabilities, the administrative user must be able to install replica FreeIPA servers for an existing FreeIPA domain.

### Enterprise Target (Fedora 28, early/mid 2018)
 * The administrative user must be able to install FreeIPA as a subordinate domain of an existing Active Directory forest.
 * The administrative user must be able to install FreeIPA replicas into a mixed FreeIPA/Active Directory forest.

### Long-term Goals
 * The administrative user should be able to deploy a new subordinate FreeIPA domain into an existing FreeIPA forest.
 * The administrative user should be able to deploy a new subordinate FreeIPA domain into an existing mixed FreeIPA/Active Directory forest.
 * The administrative user should be able to join an existing FreeIPA forest into an existing Active Directory domain forest.

## Technical Requirements
(Note: some of these may already exist)
### FreeIPA
 * An idempotent installer that can be driven by Ansible
 * Capability to enroll a machine as a replica of an existing domain.
  * This enrollment may not require preparation steps performed on a separate machine.
  * This enrollment must be possible to initiate solely from the machine requesting the enrollment.
 * Capability to enroll a machine as a domain in an existing Active Directory Forest.
  * As far as possible, this should be possible to initiate solely from the machine requesting enrollment. This may require developing PowerShell capabilities to configure the Windows machine.
 * Long-term: FreeIPA must support trusted FreeIPA domains

### Cockpit
 * Cockpit must provide a graphical user experience for executing all of the workflows described in this document.
 * Cockpit must be able to export an Ansible playbook at the end of the workflow, prior to executing the changes.
 * Cockpit must be able to import an Ansible playbook for domain creation and execute it. (Expert mode for custom changes made to the Ansible playbook).
