## Copilot instructions for NetApp Console documentation

### Repository overview
Product: NetApp Console

NetApp Console is a unified storage management platform that manages and protects data across on-premises and cloud environments. It is available as a SaaS application (standard mode), can be installed in a public cloud environment (restricted mode), or deployed on-premises or in an air-gapped environment (private mode).

### Repository structure

All documentation files are in the repository root, organized by filename prefix:

- `concept-*.adoc` – Conceptual and explanatory pages that describe product features and architecture
- `task-*.adoc` – Procedural pages with numbered steps for administrator and user tasks
- `reference-*.adoc` – Reference pages with tables, configuration details, and lookup information
- `whats-new.adoc` – Release notes landing page that includes content from `_whatsnew/`
- `faq-iam-netapp-console.adoc` – IAM frequently asked questions
- `legal-notices.adoc` – Legal notices page
- `_include/` – Reusable AsciiDoc content snippets included in multiple pages (networking requirements, endpoints, permissions, and installation steps)
- `_whatsnew/` – Dated release notes files (one per release) included into `whats-new.adoc`; all links and images must use absolute URLs or they break when the file is included into the root-level file
- `media/` – Screenshots and diagrams referenced by documentation pages
- `store-redirects/` – URL redirect configuration for renamed or moved pages

Major content groupings in the root:

- `concept-agents.adoc`, `concept-agent-install-options.adoc` – Console agent overview and deployment method comparison
- `concept-modes.adoc` – Deployment mode comparison (standard, restricted, private)
- `concept-identity-and-access-management.adoc`, `concept-iam-rbac.adoc` – IAM hierarchy and RBAC concepts
- `concept-federation.adoc` – Identity federation and SSO overview
- `concept-accounts-aws.adoc`, `concept-accounts-azure.adoc`, `concept-accounts-gcp.adoc` – Cloud provider account types and credentials
- `concept-org-partnerships.adoc` – Cross-organization resource sharing for MSPs and resellers
- `task-install-agent-*.adoc` – Agent installation procedures by cloud provider and deployment method
- `task-iam-*.adoc` – IAM management tasks (folders, projects, members, roles, resources, agents)
- `task-federation-*.adoc` – Identity provider configuration (AD FS, Microsoft Entra ID, PingFederate, SAML)
- `task-quick-start-*.adoc` – Quick-start guides for each deployment mode
- `reference-iam-*.adoc` – Role definitions and permission tables organized by data service
- `reference-networking-*.adoc` – Required network endpoints by deployment mode
- `reference-permissions-*.adoc` – Cloud provider permission requirements
- `reference-ports-*.adoc` – Required ports by cloud provider

### Product-specific context

**Architecture and components:**
- *NetApp Console SaaS application* – Cloud-hosted web UI and API; the central management plane in standard mode
- *Console agent* – Lightweight software installed in customer cloud or on-premises environments that bridges storage systems to the Console. Agents initiate all outbound communication; the Console never initiates connections to agents.
- *Storage systems* – Managed resources including on-premises ONTAP clusters, E-Series, StorageGRID, Cloud Volumes ONTAP, Amazon FSx for NetApp ONTAP, Azure NetApp Files, Google Cloud NetApp Volumes, Amazon S3, Azure Blob storage, and Google Cloud Storage
- *Data services* – Add-on capabilities including NetApp Backup and Recovery, Disaster Recovery, Ransomware Resilience, Data Classification, Copy and Sync, Replication, and Volume Caching; most require a Console agent
- *IAM hierarchy* – Organization (top level) > Folders > Projects > Resources; members are assigned roles at any level of the hierarchy

**Key concepts:**
- *Deployment modes* – Standard mode uses the cloud-hosted SaaS application with full feature access; restricted mode is installed in a public cloud with limited outbound connectivity to NetApp APIs; private mode is installed on-premises or in an air-gapped environment with no outbound connectivity to NetApp
- *Organization* – Top-level IAM container representing a company; contains folders, projects, members, roles, and resources; only one organization is created per company sign-up
- *Folders* – Optional groupings of related projects organized by location, department, or business unit; resources cannot be assigned directly to folders
- *Projects* – Core organizational units that group storage resources; resources can belong to multiple projects; users access resources through project membership
- *Resources* – Entities the Console manages: storage systems, Keystone subscriptions, some Backup and Recovery workloads, and Console agents
- *Console agent* – Required for advanced data services, Cloud Volumes ONTAP management, restricted mode, and private mode; only Organization admins can create Console agents; agents are created within a project and can be associated with additional projects
- *Identity federation* – Enables SSO using corporate credentials via SAML, AD FS, Microsoft Entra ID, or PingFederate. Not available in private mode. NetApp supports service provider-initiated (SP-initiated) SSO only.
- *Partnerships* – Cross-organization relationships that let managed service providers (MSPs) or resellers access and manage a customer's Console resources using role-driven access; the initiating organization controls which resources are shared and what roles are assigned

**Naming conventions and terminology:**
- *NetApp Console* – The product name; no article in headings; "the NetApp Console" on first body reference; "the Console" on subsequent references in the same file
- *Console agent* – Capital C, lowercase a in prose; "Console Agent" only when reflecting a UI label exactly as displayed; incorrect forms include `console agent` and `Console Agent` in body prose
- *IAM* – Identity and Access Management
- *RBAC* – Role-based access control; all Console roles follow least-privilege principles
- *NSS* – NetApp Support Site; used for account association, licensing, and support access
- *Platform roles* – Console administration permissions: Organization admin, Folder or project admin, Federation admin, Federation viewer, Partnership admin, Partnership viewer, Super admin, Super viewer, Organization viewer
- *Application roles* – Storage and monitoring permissions: Storage admin, Storage viewer, System health specialist, Operation support analyst, Google Cloud NetApp Volumes admin/viewer, Keystone admin/viewer
- *Data service roles* – Service-specific permissions such as Backup and Recovery admin/viewer, Ransomware Resilience admin/viewer, Disaster Recovery admin/viewer

**Technical constraints:**
- Console agents must initiate all communication to the Console; the Console never initiates connections to agents
- Google Cloud resources can only be managed by a Console agent deployed in Google Cloud; on-premises agents cannot manage Google Cloud resources
- Only Organization admins can create Console agents
- Federation is not available in private mode
- In restricted and private modes, the Console UI is accessed locally from an agent VM, not from the cloud-hosted SaaS application
- Private mode agents must be manually upgraded; standard and restricted mode agents with internet access upgrade automatically
- OVA-based on-premises deployment requires VMware vCenter; it cannot be installed on a bare ESXi host

### Typical user workflows

**Standard mode setup:** Prepare networking → Sign up and create organization → Associate NSS account → Deploy Console agent → Add or discover storage systems → Subscribe to data services (optional)

**IAM setup:** Create folders and projects matching business hierarchy → Add members to organization → Assign roles at appropriate hierarchy level → Add or discover resources → Associate resources with projects → Associate Console agents with projects

**Console agent deployment (from Console):** Set up networking and cloud provider permissions → Deploy agent from NetApp Console → Agent registers automatically → Verify agent status in Console

**Console agent deployment (manual):** Prepare Linux host → Install Docker or Podman → Configure networking and required endpoints → Install Console agent software → Register agent with Console → Verify connectivity

**Identity federation setup:** Verify domain ownership if federating with a domain other than your email domain → Configure identity provider to trust NetApp as service provider → Create federated connection in Console → Test connection with a test user → Enable federation

**Restricted mode setup:** Subscribe through cloud marketplace → Prepare networking → Deploy Console agent from marketplace or manually → Access Console UI from agent VM → Configure IAM and add storage systems
