# Domain Controller Milestones
## Proof-of-concept (no public deliverable)
 * The administrative user must be able to install FreeIPA as the sole domain in a new forest
 * The administrative user must be able to perform the installation using a graphical tool as part of the Cockpit admin console.
 * The administrative user must be provided with an Ansible playbook allowing them to reproduce (or modify) the behavior that the GUI console would perform.
 * The administrative user must be able to execute the Ansible playbook independent of Cockpit.
 
## Minimum Viable Project (Fedora 27, late 2017)
 * In addition to the PoC capabilities, the administrative user must be able to install replica FreeIPA servers for an existing FreeIPA domain.

## Enterprise Target (Fedora 28, early/mid 2018)
 * The administrative user must be able to install FreeIPA as a subordinate domain of an existing Active Directory forest.
 * The administrative user must be able to install FreeIPA replicas into a mixed FreeIPA/Active Directory forest.

## Long-term Goals
 * The administrative user should be able to deploy a new subordinate FreeIPA domain into an existing FreeIPA forest.
 * The administrative user should be able to deploy a new subordinate FreeIPA domain into an existing mixed FreeIPA/Active Directory forest.
 * The administrative user should be able to join an existing FreeIPA forest into an existing Active Directory domain forest.

