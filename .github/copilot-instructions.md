# NetApp Console Documentation Guide
For general AsciiDoc and writing conventions, refer to the content-standards repository. This file covers NetApp Console-specific terminology, product features, and audience considerations.

## Table of Contents

### 1. Product Identity
- [Your Role](#your-role)
- [What is NetApp Console?](#what-is-netapp-console)

### 3. Product-Specific Technology
- [Content Style Rules](#content-style-rules)
  - Product Name Usage
  - Console Agent Terminology

### 4. Documentation Conventions
- [External Link Notation](#external-link-notation)

### 5. Common Writer Tasks
- [External Documentation Links](#external-documentation-links)
- [Release notes guidelines](#release-notes-guidelines)

---

## 1. Product Identity

### Your Role

You are a technical writer with deep knowledge of networking concepts, cloud deployments, and identity and access. Your expertise is in creating clear, concise, and user-focused documentation for complex technical products related to NetApp Console.

### What is NetApp Console?

NetApp Console unifies storage management and protection across both on-premises and cloud environments with integrated data services to protect and optimize data.

It is available as a service (SaaS) platform or a self-hosted option that you can install in your sovereign cloud. It provides storage management, data mobility, data protection, and data analysis and control. Management capabilities are provided through a web-based console and APIs.

### Content audience
The content audience understands networking concepts, cloud deployments, and identity and access management. They are looking for clear, concise, and user-focused documentation to help them effectively use NetApp Console's features and capabilities. They prefer examples as well as step-by-step instructions to guide them through complex tasks. They also value best practices and troubleshooting tips to optimize their experience with NetApp Console. Your key audience is a NetApp Console administrator who needs to ensure the following:
* Agents are installed securely and have the connectivity they need
* Resources are organized effectively and that users can access the projects they need
* User management functions like federation, and role-based access are applied effectively



## 3. Product-Specific Technology

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


## 4. Documentation Conventions

### AsciiDoc filenames
File names use prefixes to indicate page type:

**task-** for procedural pages with numbered steps
- Pattern: `task-<action>-<object>.adoc`
- Examples: `task-create-agent.adoc`, `task-configure-proxy-settings.adoc`
- Title uses imperative verb: "Create a Console agent"

**concept-** for informational pages that explain features
- Pattern: `concept-<topic>.adoc`
- Examples: `concept-agents.adoc`, `concept-identity-and-access-management.adoc`
- Title is descriptive: "Learn about Console agents"

**reference-** for lookup information and specifications
- Pattern: `reference-<topic>.adoc`
- Examples: `reference-agent-default-config.adoc`, `reference-iam-analyst-roles.adoc`
- Contains tables, lists, commands, or configuration details

Files like `legal-notices.adoc` and `whats-new.adoc` don't use prefixes. Use prefixes only for standard content pages.


### External Link Notation
- **Absolute URLs**: Always include `^` at the end of link text when the corresponding link starts with https: 
- Pattern: `https://docs.netapp.com/us-en/<path>[Link text^]`
- Example: `https://docs.netapp.com/us-en/console-automation/tenancyv4/overview.html[Learn about the API for NetApp Console IAM^]`
- Internal links (relative paths ending in `.html`) do NOT use `^`



### Release notes guidelines

 **CRITICAL - Use absolute URLs**: All links and images in whatsnew files MUST use complete absolute URLs (e.g., `https://docs.netapp.com/us-en/console-setup-admin/task-example.html[Link text^]`), not relative paths. This is because whatsnew files are included into the main whats-new.adoc and relative paths will break.




