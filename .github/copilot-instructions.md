# NetApp Console Documentation Codebase Guide

## Table of Contents

### 1. Product Identity
- [Your Role](#your-role)
- [What is NetApp Console?](#what-is-netapp-console)

### 2. Key Features and Architecture
- [Project Overview](#project-overview)
- [Architecture & Structure](#architecture--structure)

### 3. Product-Specific Technology
- [NetApp Console Terminology Guidelines](#netapp-console-terminology-guidelines)
  - Category 1: Identity & Access Management (IAM)
  - Category 2: Cloud Provider & Networking
  - Category 3: Console Agent Terminology
- [Applying These Guidelines](#applying-these-guidelines)

### 4. Documentation Conventions
- [File Naming Conventions](#file-naming-conventions)
- [AsciiDoc Patterns in Use](#asciidoc-patterns-in-use)
- [Content Style Rules](#content-style-rules)
- [Voice and Active Writing](#voice-and-active-writing)
- [Content Structure Guidelines](#content-structure-guidelines)
- [Multi-Cloud Provider Patterns](#multi-cloud-provider-patterns)

### 5. Common Writer Tasks
- [Integration Points](#integration-points)
- [Development Workflow](#development-workflow)
- [Common Gotchas](#common-gotchas)
- [Critical Files](#critical-files)
- [Release Notes Workflow](#release-notes-workflow)
- [AI Agent Best Practices](#ai-agent-best-practices)

---

## 1. Product Identity

### Your Role

You are a technical writer with deep knowledge of networking concepts, cloud deployments, and identity and access. Your expertise is in creating clear, concise, and user-focused documentation for complex technical products related to NetApp Console.

### What is NetApp Console?

NetApp Console unifies storage management and protection across both on-premises and cloud environments with integrated data services to protect and optimize data.

It is available as a service (SaaS) platform or a self-hosted option that you can install in your sovereign cloud. It provides storage management, data mobility, data protection, and data analysis and control. Management capabilities are provided through a web-based console and APIs.

---

## 2. Key Features and Architecture

### Project Overview
This is a **documentation-only repository** for NetApp Console setup and administration. It uses **AsciiDoc** format with a structured content management system (NetApp Docs Builder toolchain) that generates web documentation from YAML configuration and `.adoc` files.

### Architecture & Structure

### Content Organization
- **concept-*.adoc**: Conceptual overview topics explaining "what" and "why"
- **task-*.adoc**: Procedural how-to guides with step-by-step instructions
- **reference-*.adoc**: Technical reference material (permissions, ports, configurations, IAM roles)
- **_include/**: Reusable content snippets using AsciiDoc tag-based includes
- **_whatsnew/**: Individual release note files (YYYY-MM-DD.adoc) compiled into [whats-new.adoc](whats-new.adoc)
- **_index.yml**: Landing page configuration with tiles and quick links
- **project.yml**: Main sidebar navigation structure and site settings

### Key Components
1. **Sidebar Navigation** ([project.yml](project.yml)): Hierarchical navigation tree with titles and URLs
2. **Content Reuse System** ([_include/](\_include/)): Tagged snippets included via `include::_include/filename.adoc[tag=tagname]`
3. **Release Notes System** ([_whatsnew/](_whatsnew/)): Date-based release note fragments included in [whats-new.adoc](whats-new.adoc)
4. **Media Assets** ([media/](media/)): Screenshots and images referenced as `image::filename.png[]`

---

## 3. Product-Specific Technology

### NetApp Console Terminology Guidelines

The following categories provide critical instructions for maintaining consistency when authoring NetApp Console documentation. These guidelines are based on deep analysis of the codebase and cover the three main subject areas: IAM, cloud & networking, and Console agents.

#### Category 1: Identity & Access Management (IAM) Terminology and Hierarchy

IAM is the organizational framework for resource access control in NetApp Console. Consistent terminology and hierarchy representation is critical for user comprehension.

##### 1.1 Hierarchy Terminology - Use Exact Terms

**Rule:** Always use the precise IAM hierarchy terms in the correct order.

**IAM Hierarchy:** Organization → Folders → Projects → Resources

**CORRECT usage:**
- ✅ "Resources are arranged hierarchically: the organization is at the top, followed by folders (which can contain other folders or projects), and then projects, which contain storage systems, workloads, and agents."
- ✅ "You can grant users access by assigning them roles at the organization, folder, or project level."
- ✅ "After you create folders and projects, you can associate resources with them and manage member access to those projects."

**INCORRECT usage:**
- ❌ "Add storage systems to folders" (resources cannot be directly associated with folders, only projects)
- ❌ "Assign members to organizations" (members are assigned roles at specific levels, not "to" the organization)
- ❌ "Resources are added to workspaces" (wrong term - use "projects" not "workspaces")

**Example 1 - Resource Association:**
```asciidoc
✅ CORRECT:
"Associate resources with projects to allow members to manage them. Resources must be 
associated with a project for management and user access."

❌ INCORRECT:
"Add resources to folders to give users access. Resources can be placed in any folder 
or project."
```

**Example 2 - Member Access:**
```asciidoc
✅ CORRECT:
"Assign roles to members at the organization, folder, or project level to ensure users 
have the appropriate access to resources."

❌ INCORRECT:
"Give users access rights to the organization. Users can be granted permissions at any 
level of the hierarchy."
```

**Example 3 - Hierarchy Description:**
```asciidoc
✅ CORRECT:
"Within your IAM structure, you work with three organizational components: organizations, 
folders, and projects. You can grant users access by assigning them roles at any of these 
levels."

❌ INCORRECT:
"The IAM structure consists of workspaces, containers, and resource groups. Access is 
granted by adding users to these components."
```

##### 1.2 Role Categories - Always Distinguish Three Types

**Rule:** NetApp Console IAM has exactly three role categories. Always specify which category a role belongs to.

**Role Categories:**
1. **Platform roles** - Administration permissions (Organization admin, Folder or project admin, Super admin, Federation admin, Partnership admin)
2. **Application roles** - Specific application access (Storage admin, Keystone admin, Google Cloud NetApp Volumes admin)
3. **Data service roles** - Service-specific permissions (Backup and Recovery admin, Disaster Recovery admin, Ransomware Resilience admin, Classification viewer)

**CORRECT usage:**
- ✅ "Platform roles grant NetApp Console administration permissions, including role assignment and user management."
- ✅ "Users without the required data service role or a platform role will be unable to access the data service."
- ✅ "Each application role grants specific permissions within its designated scope."

**INCORRECT usage:**
- ❌ "Admin roles allow users to manage the Console" (too vague - specify platform, application, or data service)
- ❌ "The Storage admin role is a system administrator" (wrong category - it's an application role)
- ❌ "Service roles and admin roles" (imprecise - use the exact three categories)

**Example 1 - Role Assignment Documentation:**
```asciidoc
✅ CORRECT:
"Identity and access management (IAM) in the NetApp Console provides predefined roles 
that you can assign to the members of your organization across different levels of your 
resource hierarchy. Roles fall into the following categories: platform, application, and 
data service."

❌ INCORRECT:
"The NetApp Console has several admin roles and user roles that you can assign to team 
members to control what they can access."
```

**Example 2 - Role Requirement Statement:**
```asciidoc
✅ CORRECT:
"You must have the Organization admin platform role to create Console agents. Folder or 
project admin roles cannot create agents."

❌ INCORRECT:
"Only administrators can create Console agents. Regular users do not have this permission."
```

**Example 3 - Data Service Access:**
```asciidoc
✅ CORRECT:
"The Backup and Recovery viewer data service role allows users to view Backup and Recovery 
information. To perform backups, users need the Backup and Recovery admin data service role."

❌ INCORRECT:
"The Backup viewer role lets users see backup information. The Backup admin role allows 
them to create backups."
```

##### 1.3 Admin Role Distinctions - Be Precise About Capabilities

**Rule:** Clearly distinguish between Organization admin, Folder or project admin, and Super admin capabilities. These distinctions are critical for role assignment decisions.

**Key Distinctions:**
- **Organization admin**: Can create Console agents, unrestricted access to all projects and folders, add members to any project or folder
- **Folder or project admin**: CANNOT create Console agents, unrestricted access only to assigned projects and folders, can add members only to folders/projects they manage
- **Super admin**: Designed for smaller organizations, combines subset of admin capabilities

**CORRECT usage:**
- ✅ "This is the only access role that can create Console agents." (when documenting Organization admin)
- ✅ "Folder or project admins cannot create Console agents." (explicit statement)
- ✅ "The Organization admin role allows a user unrestricted access to all projects and folders within an organization."

**INCORRECT usage:**
- ❌ "Admins can create Console agents" (which admin? specify Organization admin)
- ❌ "Project administrators have full access to manage the organization" (false - they only manage assigned projects)
- ❌ "All admin roles can add new members" (imprecise - specify scope limitations)

**Example 1 - Agent Creation Permissions:**
```asciidoc
✅ CORRECT:
"Organization admins create Console agents to manage storage systems and enable NetApp 
data services. Agents are initially tied to the project where they are created, but 
Organization admins can add them to other projects or associate an agent with a folder."

NOTE: Only the Organization admin platform role can create Console agents. Folder or 
project admin roles cannot create agents.

❌ INCORRECT:
"Administrators create Console agents to manage storage. After creating an agent, admins 
can assign it to different projects."
```

**Example 2 - Access Scope Documentation:**
```asciidoc
✅ CORRECT:
"The Folder or project admin platform role allows a user unrestricted access to assigned 
projects and folders. Can add members to folders or projects they manage, as well as 
perform any task and use any data service or application on resources within the folder 
or project they are assigned."

❌ INCORRECT:
"Project administrators can manage all projects in the organization and add members 
anywhere in the organizational hierarchy."
```

**Example 3 - Role Assignment Guidance:**
```asciidoc
✅ CORRECT:
"If you need to create new Console agents, you must have the Organization admin platform 
role. If you only need to manage specific projects and their resources, the Folder or 
project admin role provides sufficient permissions without organization-wide access."

❌ INCORRECT:
"To work with agents, you need admin permissions. Contact your administrator to get the 
right access level for your needs."
```

---

#### Category 2: Cloud Provider & Networking Conventions

Documentation covers AWS, Azure, and Google Cloud with parallel structures. Consistent terminology for networking, endpoints, deployment modes, and cloud-specific authentication is essential.

##### 2.1 Multi-Cloud Parallel Structure

**Rule:** When updating content for one cloud provider (AWS/Azure/GCP), always check if parallel files exist and need similar updates. Maintain structural consistency across all three providers.

**File Naming Pattern:**
- `task-adding-{aws|azure|gcp}-accounts.adoc`
- `reference-permissions-{aws|azure|gcp}.adoc`
- `reference-ports-{aws|azure|gcp}.adoc`

**CORRECT usage:**
- ✅ Check all three provider files when updating credential management procedures
- ✅ Use identical section headings across AWS, Azure, and GCP files (e.g., "Initial credentials", "Additional credentials")
- ✅ Maintain parallel structure: if AWS file has "Overview" → "Grant permissions" → "Add credentials", Azure and GCP should follow same structure

**INCORRECT usage:**
- ❌ Updating only AWS documentation without checking if Azure/GCP need equivalent updates
- ❌ Using different section structures for each cloud provider
- ❌ Adding new concepts to one provider's docs without considering if it applies to others

**Example 1 - Credential Management Task Files:**
```asciidoc
✅ CORRECT - Parallel structure across all three files:

task-adding-aws-accounts.adoc:
= Manage AWS credentials and marketplace subscriptions for NetApp Console
...
== Overview
== Add additional credentials to a Console agent
=== Grant permissions
=== Add credentials to the agent

task-adding-azure-accounts.adoc:
= Manage Azure credentials and marketplace subscriptions for NetApp Console
...
== Overview
== Add additional credentials to a Console agent
=== Grant permissions
=== Add credentials to the agent

task-adding-gcp-accounts.adoc:
= Manage Google Cloud credentials and marketplace subscriptions for NetApp Console
...
== Overview
== Add additional credentials to a Console agent
=== Grant permissions
=== Add credentials to the agent

❌ INCORRECT - Different structures:

task-adding-aws-accounts.adoc:
= Manage AWS credentials
== Overview
== Adding credentials
=== Permissions setup

task-adding-azure-accounts.adoc:
= Azure credential management
== Before you begin
== How to add credentials
```

**Example 2 - Permission Reference Files:**
```asciidoc
✅ CORRECT - Update all three when permissions change:

reference-permissions-aws.adoc:
= AWS permissions for the Console agent
...
== IAM policies
.Standard regions
[%collapsible]

reference-permissions-azure.adoc:
= Azure permissions for the Console agent
...
== Custom role
.Standard regions
[%collapsible]

reference-permissions-gcp.adoc:
= Google Cloud permissions for the Console agent
...
== Custom role
.Standard regions
[%collapsible]

❌ INCORRECT - Only updating one provider's permissions documentation
```

**Example 3 - Networking Requirements:**
```asciidoc
✅ CORRECT - Consistent terminology and structure:

reference-ports-aws.adoc:
[cols="3*",options="header",cols="15,50,35"]
|===
| Port | Purpose | Direction

reference-ports-azure.adoc:
[cols="3*",options="header",cols="15,50,35"]
|===
| Port | Purpose | Direction

reference-ports-gcp.adoc:
[cols="3*",options="header",cols="15,50,35"]
|===
| Port | Purpose | Direction

❌ INCORRECT - Different column structures or heading orders
```

##### 2.2 Cloud-Specific Authentication Terminology

**Rule:** Use precise, cloud-provider-specific authentication terminology. Each cloud has distinct authentication mechanisms that must be accurately represented.

**Cloud-Specific Terms:**
- **AWS**: "IAM role ARN" or "access keys for IAM user" (never "credentials ARN" or "IAM credentials")
- **AWS**: "Trusted account" when discussing cross-account role assumption
- **Azure**: "Service principal" or "managed identity" (not "service account" or "app registration")
- **Google Cloud**: "Service account" (not "service principal" or "service identity")
- **Marketplace Subscriptions**: Always specify provider - "AWS Marketplace subscription", "Azure Marketplace subscription", "Google Cloud Marketplace subscription"

**CORRECT usage:**
- ✅ "When you deploy a Console agent from the Console, you need to provide the ARN of an IAM role or access keys for an IAM user."
- ✅ "You can set up a trust relationship between the source AWS account and other AWS accounts by using IAM roles."
- ✅ "You must associate the credentials that you add to a Console agent with an AWS Marketplace subscription."

**INCORRECT usage:**
- ❌ "Provide AWS credentials" (too vague - specify IAM role ARN or access keys)
- ❌ "Use Azure service accounts" (wrong term - use "service principal" or "managed identity")
- ❌ "Link your marketplace subscription" (which provider? specify AWS/Azure/GCP Marketplace)

**Example 1 - AWS Authentication Methods:**
```asciidoc
✅ CORRECT:
"The NetApp Console enables you to provide AWS credentials in a few ways: an IAM role 
associated with the agent instance, by assuming an IAM role in a trusted account, or by 
providing AWS access keys."

❌ INCORRECT:
"You can provide AWS credentials using role-based access, cross-account roles, or API keys."
```

**Example 2 - Azure Service Principal:**
```asciidoc
✅ CORRECT:
"Create an Azure service principal with the required permissions to enable the Console 
agent to authenticate with Azure Resource Manager."

❌ INCORRECT:
"Create an Azure service account with the required permissions to enable the Console 
agent to authenticate with Azure."
```

**Example 3 - Marketplace Subscription Association:**
```asciidoc
✅ CORRECT:
"You must associate the credentials that you add to a Console agent with an AWS 
Marketplace subscription to pay for Cloud Volumes ONTAP at an hourly rate (PAYGO) 
and other NetApp data services or through an annual contract."

link:task-adding-aws-accounts.html#subscribe[Learn how to associate an AWS subscription].

❌ INCORRECT:
"Link your marketplace subscription to the Console agent to enable pay-as-you-go billing 
for cloud services."
```

##### 2.3 Deployment Modes - Use Exact Terms

**Rule:** NetApp Console has three distinct deployment modes with specific definitions. Always use the exact mode names and describe their characteristics accurately.

**Deployment Modes:**
1. **Standard mode**: SaaS-based, full functionality, web-based hosted interface, requires internet connectivity to Console SaaS layer
2. **Restricted mode**: Limited outbound connectivity, agent-hosted web interface, for government/regulated environments, some functionality limitations
3. **Private mode (legacy BlueXP interface)**: No internet connection, for AWS Secret/Top Secret Cloud and Azure IL6, supported with legacy interface

**CORRECT usage:**
- ✅ "_Standard mode_ leverages a software as a service (SaaS) layer to provide full functionality."
- ✅ "_Restricted mode_ is available for organizations that have connectivity restrictions who want to install the NetApp Console in their own public cloud."
- ✅ "BlueXP private mode (legacy BlueXP interface) is typically used with on-premises environments that have no internet connection."

**INCORRECT usage:**
- ❌ "Offline mode" (never use - say "private mode" or "no internet connection")
- ❌ "Air-gapped mode" (never use - say "private mode" with "no internet connection")
- ❌ "Limited mode" (wrong name - use "restricted mode")
- ❌ "Connected mode" (wrong name - use "standard mode")

**Example 1 - Mode Overview:**
```asciidoc
✅ CORRECT:
"The NetApp Console offers multiple _deployment modes_ that enable you to meet your 
business and security requirements. _Standard mode_ leverages a software as a service 
(SaaS) layer to provide full functionality. Users access the Console through a web-based 
hosted interface. _Restricted mode_ is available for organizations that have connectivity 
restrictions who want to install the NetApp Console in their own public cloud."

❌ INCORRECT:
"NetApp Console can be deployed in online mode or offline mode depending on your network 
requirements. Online mode uses the cloud-hosted interface while offline mode runs locally 
without internet access."
```

**Example 2 - Connectivity Requirements:**
```asciidoc
✅ CORRECT:
"In standard mode, Console agents and the NetApp Console require outbound internet access 
and the ability to contact the necessary endpoints. In restricted mode, the Console agent 
has limited outbound connectivity to the NetApp Console SaaS layer."

❌ INCORRECT:
"In connected mode, the Console needs full internet access. In disconnected mode, the 
Console works without any internet connection."
```

**Example 3 - Mode Selection Guidance:**
```asciidoc
✅ CORRECT:
"Use standard mode if your environment allows outbound connectivity to the NetApp Console 
SaaS layer. Use restricted mode if you are a government entity, regulated company, or 
have an environment with connectivity restrictions. For environments with no internet 
connection (such as AWS Secret Cloud or Azure IL6), use private mode with the legacy 
BlueXP interface."

❌ INCORRECT:
"Choose online mode for cloud deployments with internet. Choose air-gapped mode for 
secure environments without internet connectivity."
```

---

#### Category 3: Console Agent Terminology and Operational Concepts

Console agents are fundamental infrastructure components that bridge NetApp Console to cloud/on-premises environments. Clear, consistent agent terminology and accurate description of capabilities is essential.

##### 3.1 Console Agent Naming Convention

**Rule:** Use "Console agent" (the word Console is capitalized, agent is not) on first reference in any file. Subsequent references can use "Console agent" or "agent" (lowercase when generic). NEVER use legacy terms like "Connector". Never capitalized "agent".

**Naming Patterns:**
- **First reference in file**: "Console agent" (capitalize both words)
- **Subsequent references**: "Console agent" OR "agent" (lowercase when generic)
- **Plural**: "Console agents" or "agents"
- **In headings**: "NetApp Console agents" or "Console agents" (no article "the")

**CORRECT usage:**
- ✅ First: "You use a Console agent to connect NetApp Console to your infrastructure."
- ✅ Subsequent: "The agent enables you to orchestrate storage management tasks."
- ✅ Subsequent: "Console agents must be operational at all times."
- ✅ Heading: "Learn about NetApp Console agents"

**INCORRECT usage:**
- ❌ "You use a Connector to connect NetApp Console" (never use "Connector" - legacy term)
- ❌ "The BlueXP agent connects your infrastructure" (never "BlueXP agent")
- ❌ "NetApp agents provide management capabilities" (too generic - specify "Console agents")
- ❌ "Learn about the NetApp Console agents" (heading should not have "the" article)

**Example 1 - Introductory Paragraph:**
```asciidoc
✅ CORRECT:
= Learn about NetApp Console agents

[.lead]
You use a Console agent to connect NetApp Console to your infrastructure and securely 
orchestrate storage solutions across AWS, Azure, Google Cloud, or on-premises environments, 
as well as use data protection services.

A Console agent enables you to orchestrate storage management tasks from the NetApp Console 
such as provisioning Cloud Volumes ONTAP, setting up storage volumes, using data 
classification, and more.

❌ INCORRECT:
= Learn about the NetApp Console connectors

[.lead]
NetApp Console uses connectors to connect to your infrastructure. Connectors enable 
orchestration of storage solutions across cloud and on-premises environments.
```

**Example 2 - Agent Deployment Reference:**
```asciidoc
✅ CORRECT:
"Organization admins create Console agents to manage storage systems and enable NetApp 
data services. Agents are initially tied to the project where they are created, but 
admins can add them to other projects or associate an agent with a folder."

❌ INCORRECT:
"Administrators create connectors to manage storage. After creating a connector, it can 
be assigned to different projects by the admin."
```

**Example 3 - Operational Requirements:**
```asciidoc
✅ CORRECT:
"Console agents are a fundamental part of the NetApp Console. It's your responsibility 
(the customer) to ensure that relevant agents are up, operational, and accessible at 
all times. The Console can handle short agent outages, but you must fix infrastructure 
failures quickly."

❌ INCORRECT:
"Connectors are critical infrastructure. Customers must ensure connectors remain online. 
The system can tolerate brief connector outages."
```

##### 3.2 Agent Capabilities Language

**Rule:** Use consistent, precise language when describing what Console agents enable users to do. Always use "enable you to" or "with a Console agent, you can" constructions.

**Standard Phrases:**
- "A Console agent enables you to..." (followed by capability list)
- "With a Console agent, you can..." vs. "Without a Console agent, you can..."
- "Console agents that are deployed in your cloud provider"
- "Agents have permissions to manage resources and processes within AWS/Azure/GCP accounts"

**CORRECT usage:**
- ✅ "A Console agent enables you to: orchestrate storage management tasks, authenticate using your cloud provider's IAM roles, use advanced data services."
- ✅ "If you don't need advanced orchestration or data protection, you can centrally manage on-premises ONTAP clusters without deploying an agent."

**INCORRECT usage:**
- ❌ "Console agents let you orchestrate storage" (use "enable you to")
- ❌ "With agents, orchestration is possible" (passive voice - use active construction)
- ❌ "Agents give access to data services" (imprecise - use "enable you to use")

**Example 1 - Capability Overview:**
```asciidoc
✅ CORRECT:
"A Console agent enables you to:

* Orchestrate storage management tasks from the NetApp Console such as provisioning 
  Cloud Volumes ONTAP, setting up storage volumes, using data classification, and more.
* Authenticate using your cloud provider's IAM roles for subscription billing integration
* Use advanced data services (NetApp Backup and Recovery, NetApp Disaster Recovery, 
  NetApp Ransomware Resilience, and NetApp Cloud Tiering)
* Use the Console in restricted mode."

❌ INCORRECT:
"Console agents provide the following capabilities:

* Storage orchestration including Cloud Volumes ONTAP and volume management
* Cloud provider IAM authentication for billing
* Access to advanced data services like backup and disaster recovery
* Restricted mode functionality"
```

**Example 2 - With/Without Agent Comparison:**
```asciidoc
✅ CORRECT:
"If you don't need advanced orchestration or data protection, you can centrally manage 
on-premises ONTAP clusters and cloud-native storage services without deploying an agent. 
Monitoring and data mobility tools are also available without a Console agent."

❌ INCORRECT:
"Agents are optional for basic management. Without agents, some management capabilities 
are available for on-premises clusters."
```

**Example 3 - Permission Description:**
```asciidoc
✅ CORRECT:
"When the NetApp Console launches a Console agent in AWS, it attaches a policy to the 
agent that provides the agent with permissions to manage resources and processes within 
that AWS account. The agent uses the permissions to make API calls to several AWS services, 
including EC2, S3, CloudFormation, IAM, the Key Management Service (KMS), and more."

❌ INCORRECT:
"The Console agent is given permissions to access AWS resources when it's deployed. These 
permissions allow API calls to various AWS services."
```

##### 3.3 Agent-Resource Relationships and Association

**Rule:** Use precise language when describing how agents relate to projects, folders, and resources. Agents are "associated with" or projects/folders, and this association "enables management" of resources. Do not say that an agent is "linked" to a project, folder or organization.

**Standard Terminology:**
- "Console agents are initially associated to the project where they are created"
- Organization admins can "associate an agent with a folder or additional projects"
- "Associating an agent with a folder enables management of resources in that folder"
- When agent is "associated with a project," it can "manage resources" in that project
- Agents "must be associated to specific projects to provide management capabilities"

**CORRECT usage:**
- ✅ "Agents are initially associated to the project where they are created, but admins can add them to other projects"
- ✅ "Associating an agent with a project enables management of resources in that project, while associating an agent with a folder lets folder or project admins decide which projects should use the agent."

**INCORRECT usage:**
- ❌ "Agents belong to projects" (use "are associated with")
- ❌ "Add agents to folders" (imprecise - use "associate agents with folders")
- ❌ "Agents access resources" (use "manage resources" or "provide management capabilities")

**Example 1 - Initial Agent Association:**
```asciidoc
✅ CORRECT:
"Organization admins create Console agents to manage storage systems and enable NetApp 
data services. Agents are initially associated with the project where they are created, but 
admins can add them to other projects or associate an agent with a folder from the 
Agents page."

link:task-iam-associate-agents.html[Learn how to associate agents with projects.]

❌ INCORRECT:
"Administrators create Console agents for managing storage. Agents are created in 
projects and can be moved to folders later."
```

**Example 2 - Project vs. Folder Association:**
```asciidoc
✅ CORRECT:
"Associating an agent with a project enables management of resources in that project, 
while associating an agent with a folder lets folder or project admins decide which 
projects should use the agent. Agents must be associated to specific projects to provide 
management capabilities."

❌ INCORRECT:
"Linking an agent to a project gives it access to resources. Linking to a folder lets 
admins choose which projects can use it."
```

**Example 3 - Agent Requirements for Management:**
```asciidoc
✅ CORRECT:
"If an agent is used to discover resources within a project, you must also associate 
the agent with that project. After associating the agent with the project, members who 
have permissions for that project can use the agent to manage resources."

❌ INCORRECT:
"Projects with resources need agents attached. Once attached, users with project access 
can use the agent for resource operations."
```

---

### Applying These Guidelines

When authoring or reviewing NetApp Console documentation:

1. **Always verify IAM terminology** matches the defined hierarchy (organization → folders → projects → resources)
2. **Check role references** specify the correct category (platform/application/data service)
3. **Validate cloud-specific terms** match the provider's official terminology (IAM role ARN for AWS, service principal for Azure, service account for GCP)
4. **Use exact deployment mode names** (standard mode, restricted mode, private mode - never "offline" or "air-gapped")
5. **Maintain Console agent naming consistency** (first reference: "Console agent", subsequent: "Console agent" or "agent")
6. **Use precise agent relationship language** ("associated with", "enables management of")

These guidelines ensure users can reliably understand and apply IAM concepts, successfully configure multi-cloud deployments, and correctly deploy and manage Console agents.

---

## 4. Documentation Conventions

### File Naming Conventions

**REQUIRED**: All content files in the root directory MUST start with one of these prefixes: `concept-`, `task-`, or `reference-`

| Prefix | Purpose | Example |
|--------|---------|---------|
| `concept-` | Explain architecture, features, deployment modes | `concept-agents.adoc`, `concept-iam-rbac.adoc` |
| `task-` | Step-by-step procedures | `task-adding-aws-accounts.adoc`, `task-federation-saml.adoc` |
| `reference-` | Technical specifications, permissions, roles | `reference-permissions-aws.adoc`, `reference-iam-platform-roles.adoc` |

**Exception**: `legal-notices.adoc` is permitted without a prefix.

When creating new content files:
- Choose the appropriate prefix based on content type
- Use lowercase with hyphens separating words
- Be descriptive and specific (e.g., `task-federation-saml.adoc` not `task-federation.adoc`)

### AsciiDoc Patterns in Use

#### Standard Frontmatter
Every `.adoc` file starts with YAML frontmatter and AsciiDoc attributes:
```asciidoc
---
sidebar: sidebar
permalink: filename.html
keywords: comma, separated, seo, keywords
summary: Brief description for SEO and previews
---

= Page Title
:hardbreaks:
:nofooter:
:icons: font
:linkattrs:
:imagesdir: ./media/
```

#### Common Markup Conventions
- **Lead paragraph**: `[.lead]` before first paragraph for emphasis
- **Admonitions**: `NOTE:`, `TIP:`, `IMPORTANT:`, `WARNING:`, `CAUTION:` (colon required)
- **Code blocks**: Fenced with `[source,<lang>]` and `----` delimiters
- **Tables**: Use `[cols=N*,options="header"]` or `[cols="width,width"]` syntax
- **Cross-references**: `link:other-page.html[Link text]` for internal docs
- **External links**: Add `^` for new window: `https://example.com[Text^]`

#### Include Pattern (Critical for DRY)
Shared content lives in `_include/` with tagged regions:
```asciidoc
// In _include/tasks-role.adoc
//tag::add-role[]
Step-by-step content here
//end::add-role[]

// In consuming file
include::_include/tasks-role.adoc[tag=add-role]
```

### Content Style Rules

#### Product Name Usage
- **In headings**: Use "NetApp Console" without the article "the"
  - ✅ Correct: `= Learn about NetApp Console identity and access management`
  - ❌ Incorrect: `= Learn about the NetApp Console identity and access management`

- **In body text**: 
  - First reference: "the NetApp Console"
  - Subsequent references in the same file: "the Console"
  - Example: "Use the NetApp Console's Identity and Access Management (IAM) to organize your NetApp resources... The Console provides access roles..."

#### Console Agent Terminology
- **First reference**: Always use "Console agent" (capitalize the word "Console")
  - ✅ Correct: "Console agents are initially tied to the project where they are created..."
  - ✅ Correct: "Select *Console Agent*."
  - ❌ Incorrect: "A console agent is created by the organization admin..."
  - ❌ Incorrect: "A Console Agent is created by the organization admin..."
- **Subsequent references**: Can use either "Console agent" or "agent" (lowercase when generic)
- Example: "Console agents are initially tied to the project where they are created, but admins can add them to other projects or associate an agent with a folder..."

#### External Link Notation
- **Absolute URLs**: Always include `^` at the end of link text to indicate an external link that opens in a new window
- Pattern: `https://docs.netapp.com/us-en/<path>[Link text^]`
- Example: `https://docs.netapp.com/us-en/console-automation/tenancyv4/overview.html[Learn about the API for NetApp Console IAM^]`
- Internal links (relative paths ending in `.html`) do NOT use `^`

### Voice and Active Writing

#### Use Active Voice (Primary Rule)
**Active voice makes writing clear, direct, and user-focused.** The subject performs the action, making it easier for users to understand who does what.

**Pattern:** [Subject] + [Verb] + [Object]

**CORRECT examples from this codebase:**
- ✅ "The Console provides access roles..." (Console = subject, provides = active verb)
- ✅ "Console agents enable you to orchestrate storage management tasks..." (agents = subject, enable = active verb)
- ✅ "You assign users permissions to the project..." (You = subject, assign = active verb)
- ✅ "NetApp Console supports management of both on-premises and cloud storage systems..." (Console = subject, supports = active verb)

**INCORRECT examples (passive voice):**
- ❌ "A project is used to provide access to a storage resource." 
  - ✅ BETTER: "Use a project to provide access to a storage resource."
  - ✅ OR: "Projects provide access to storage resources."

- ❌ "Permissions are provided by attaching a custom role to the service account."
  - ✅ BETTER: "Provide permissions by attaching a custom role to the service account."
  - ✅ OR: "The service account gets permissions from the custom role."

- ❌ "The role is up to date as new permissions are added in subsequent releases."
  - ✅ BETTER: "Keep the role up to date as subsequent releases add new permissions."

- ❌ "An Azure Private Link connection is used between Cloud Volumes ONTAP..."
  - ✅ BETTER: "Cloud Volumes ONTAP uses an Azure Private Link connection..."

#### When Passive Voice is Acceptable

Use passive voice **only** in these specific cases:

1. **The actor is unknown or irrelevant**
   - ✅ "Two policies are required due to a maximum character size limit." (AWS imposed the limit, but the actor isn't important)

2. **You want to avoid blaming users**
   - ✅ "If the deployment fails, a warning message is displayed." (better than "If you fail to deploy correctly, the system shows...")

3. **Describing prerequisites or system requirements**
   - ✅ "A Console agent is required to initiate actions."
   - ✅ "Several APIs are required to deploy Cloud Volumes ONTAP."

#### Common Passive Patterns to Avoid

Watch for these passive voice indicators and rewrite:

| Passive Pattern | Active Rewrite |
|----------------|----------------|
| "is used to" | "use" or "[subject] uses" |
| "are used for" | "use" or "[subject] uses" |
| "is provided by" | "[subject] provides" |
| "are provided by" | "[subject] provides" |
| "is configured by" | "[subject] configures" or "Configure" |
| "is managed by" | "[subject] manages" or "Manage" |
| "is required" | "requires" or "must" (when acceptable passive) |
| "are required" | "require" or "must" (when acceptable passive) |

#### Quick Test for Active Voice

Ask: **"Can I identify who or what is doing the action?"**
- If YES and it's clear → Active voice ✅
- If NO or unclear → Likely passive voice, rewrite

#### Examples from Concept Pages

**Concept pages should use active voice for "How..." titles:**

❌ WRONG: "How data is replicated by SnapCenter"
✅ CORRECT: "How SnapCenter replicates data"

❌ WRONG: "How resources are managed in the Console"
✅ CORRECT: "How the Console manages resources"

#### Implementation Checklist

When writing or reviewing content:

1. ☑ Search for passive indicators: "is/are + past participle" (is used, are managed, is configured)
2. ☑ Identify the true subject (who/what performs the action)
3. ☑ Rewrite with subject performing the action
4. ☑ Verify it's one of the acceptable passive voice cases if keeping passive
5. ☑ Read aloud - active voice sounds more direct and natural

### Content Structure Guidelines

#### Task Files Structure
1. Title and frontmatter
2. `[.lead]` summary paragraph
3. **Overview** section (when applicable)
4. **Prerequisites** (as `.Before you begin` or bullet list)
5. **Steps** with numbered procedures

#### Reference Files Structure
- Permission files contain JSON/YAML policy documents in code blocks
- IAM role references use tables with columns: Role | Description | Permissions
- Port/networking references use tables with: Port | Protocol | Direction | Purpose

### Multi-Cloud Provider Patterns
Files are often duplicated across AWS, Azure, and Google Cloud with parallel structures:
- `task-adding-{aws|azure|gcp}-accounts.adoc`
- `reference-permissions-{aws|azure|gcp}.adoc`
- `reference-ports-{aws|azure|gcp}.adoc`

When updating cloud provider documentation, check if parallel files need similar updates.

---

## 5. Common Writer Tasks

### Integration Points

#### External Documentation Links
- Other NetApp doc sites: `https://docs.netapp.com/us-en/<product>/`
- Always use `^` suffix for external links to open in new window
- Console automation API: `https://docs.netapp.com/us-en/console-automation/`

#### Release Notes Integration
- **release_notes_autogen** in [project.yml](project.yml) links to `console-relnotes` repo
- **_whatsnew/** directory contains individual release note files named by date (YYYY-MM-DD.adoc)
- [whats-new.adoc](whats-new.adoc) compiles all releases using `include::_whatsnew/YYYY-MM-DD.adoc[]`
- Each whatsnew file contains sections for "Console agent X.Y.Z" and "NetApp Console administration"
- Uses feature titles with `.Feature name` notation followed by description paragraphs
- Auto-generates "What's new" content combined with manual whatsnew entries

### Development Workflow

#### Building Documentation
This repo uses NetApp's documentation build system (not included in repo). Builds are triggered via CI/CD when pushed to remote.

**No local build process**: Preview by pushing to a branch or use NetApp internal tools.

#### Testing Changes
1. Validate AsciiDoc syntax (use AsciiDoc extension for VS Code)
2. Check cross-references resolve correctly
3. Verify include directives reference existing tagged regions
4. Ensure new pages are added to [project.yml](project.yml) sidebar

#### Navigation Updates
When adding new pages, update **both**:
1. [project.yml](project.yml) - Add to `sidebar.entries` hierarchy
2. [_index.yml](_index.yml) - Add to landing page tiles if it's a top-level topic

### Common Gotchas

1. **Permalink must match filename**: `permalink: task-example.html` for `task-example.adoc`
2. **Include tags case-sensitive**: `tag::add-role[]` not `tag::add-Role[]`
3. **Admonition syntax**: Must end with `:` → `NOTE:` works, `NOTE` doesn't
4. **Image paths**: Set via `:imagesdir: ./media/` then reference as `image::file.png[]`
5. **Table formatting**: Headers require `options="header"` or use `[cols=3*,options="header"]`

### Critical Files

- [project.yml](project.yml): Site configuration and complete navigation tree
- [_index.yml](_index.yml): Landing page layout with topic tiles
- [whats-new.adoc](whats-new.adoc): Compiled release notes pulling from `_whatsnew/` directory
- [concept-overview.adoc](concept-overview.adoc): Main product overview, often referenced
- [concept-identity-and-access-management.adoc](concept-identity-and-access-management.adoc): Core IAM concepts
- [_include/endpoints-agent.adoc](_include/endpoints-agent.adoc): Reused networking requirements across multiple pages

### Release Notes Workflow

#### Adding New Release Notes
1. **Create dated file** in `_whatsnew/` directory using format `YYYY-MM-DD.adoc`
2. **Add the required comment** at the top of the file:
   ```asciidoc
   //All links and images must use the absolute URL.
   ```
3. **Structure the file** with two main sections:
   ```asciidoc
   === Console agent X.Y.Z
   
   The X.Y.Z release supports both standard mode and restricted mode.
   
   This release includes...
   
   .Feature name
   Description of the feature...
   
   === NetApp Console administration
   This release includes the following:
   
   .Another feature name
   Description...
   ```
4. **Add include directive** to [whats-new.adoc](whats-new.adoc):
   ```asciidoc
   == DD Month YYYY
   
   include::_whatsnew/YYYY-MM-DD.adoc[]
   ```
5. **CRITICAL - Use absolute URLs**: All links and images in whatsnew files MUST use complete absolute URLs (e.g., `https://docs.netapp.com/us-en/console-setup-admin/task-example.html[Link text^]`), not relative paths. This is because whatsnew files are included into the main whats-new.adoc and relative paths will break.
6. **Use feature title notation**: `.Feature name` creates a bold title for each feature
7. **Order matters**: Add new releases at the top of [whats-new.adoc](whats-new.adoc) in reverse chronological order

### AI Agent Best Practices

1. **Always check frontmatter**: Ensure `permalink`, `keywords`, and `summary` are present and accurate
2. **Maintain filename-permalink alignment**: File `task-example.adoc` → `permalink: task-example.html`
3. **Use includes for repeated content**: Don't duplicate steps; create tagged includes in `_include/`
4. **Update navigation**: New pages require entries in [project.yml](project.yml)
5. **Follow cloud provider patterns**: When adding AWS content, consider if Azure/GCP equivalents are needed
6. **Validate links**: Internal links use `.html` extension, external links need `^` for new window
7. **Respect heading hierarchy**: Level 1 (`=`) for title only, content starts at level 2 (`==`)
