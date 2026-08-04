## Copilot instructions for Amazon FSx for NetApp ONTAP documentation

### Repository overview
Product: Amazon FSx for NetApp ONTAP

*Amazon FSx for NetApp ONTAP* is a fully managed AWS service that runs file systems powered by the NetApp ONTAP storage operating system. This repository documents how to create, discover, manage, replicate, and support FSx for ONTAP systems from the *NetApp Console*.

### Repository structure
- `start/` – Concept and quick-start topics for Amazon FSx for NetApp ONTAP management in the NetApp Console.
- `requirements/` – AWS credentials, IAM role, and permission setup required before creating or managing file systems.
- `use/` – Core task topics for creating or discovering systems, managing them, replicating data, monitoring operations, removing systems from projects, and deleting file systems.
- `support/` – Support registration and help topics for NetApp Console-related support workflows.
- `_include/` – Shared include directory; currently a placeholder and some procedures reference include content stored in other NetAppDocs repositories.
- `_whatsnew/` – Date-stamped release note source files for the What's New page.
- `store-redirects/` – Redirect stub topics for renamed or moved pages.
- `media/` – Images used in UI navigation and task topics.

### Product-specific context
**Architecture and components:**
- *NetApp Console* is the management entry point for the workflows documented in this repository.
- *NetApp Workload Factory* manages the AWS credentials and permissions used for FSx for ONTAP operations, and many file-system operations route from the Console into Workload Factory.
- *ONTAP System Manager* is another management path for an FSx for ONTAP file system from the Console and requires a *Console agent* or *link*.
- A *Console agent* is NetApp software deployed in a cloud or on-premises network, and a *link* uses AWS Lambda to establish connectivity between a NetApp Console account and one or more FSx for ONTAP file systems.
- A *storage VM* is created with a file system and is the unit used for volume management and some replication and migration operations.
- *Volumes* belong to a storage VM; replicated target volumes are *DP* volumes named `{OriginalVolumeName}_copy`.

**Key concepts:**
- *Discover* adds an existing FSx for ONTAP file system to the Console; it does not create a new AWS file system.
- *Remove from project* dissociates a file system from one project so it can be associated with another project in the same account.
- *Delete* removes the FSx for ONTAP file system only after dependent volumes, storage VMs, and replication relationships are removed.
- Replication is supported between *FSx for ONTAP* file systems and on-premises *ONTAP* systems or *Cloud Volumes ONTAP* systems.
- Migration replication requires three operations: create the replication relationship, initialize it, and then cut over to migrate storage VM data and configuration settings.
- Advanced features such as replication management, SMB/CIFS share and NFS export policy management, iSCSI volume management, snapshot policies, volume autogrow, clone management, well-architected status, and *NetApp Autonomous Ransomware Protection (ARP/AI)* require a *Console agent* or *link*.

**Naming conventions and terminology:**
- *FSx for ONTAP* is the repository's standard shorthand for *Amazon FSx for NetApp ONTAP*.
- *Storage* is the Workload Factory capability that must be enabled when adding credentials for FSx for ONTAP management.
- *SVM* means *storage VM* and *DP* means *data protection*.
- *Systems page*, *Discoverable systems*, *Replication relationships*, *Quick create*, and *Advanced create* are UI terms used throughout the procedures.
- *Codebox* is the automation output in the UI and exposes *REST API*, *CloudFormation*, and *Terraform* options for file-system creation.

### Typical user workflows
**Initial setup:** Add AWS credentials and IAM role → optionally deploy a *Console agent* or create a *link* → create or discover an FSx for ONTAP file system → manage it from the *Systems* page

**Create or discover a system:** Open *Storage* management → create a file system with *Quick create* or *Advanced create*, or discover an existing system → add it to the *Systems* page → manage it with Workload Factory or System Manager

**Replication or migration:** Associate a *link* when required → create the replication relationship → initialize the baseline transfer → cut over for migration use cases

**Project reassociation:** Discover a file system → remove it from a project without deleting it → rediscover and associate it with another project in the same account
