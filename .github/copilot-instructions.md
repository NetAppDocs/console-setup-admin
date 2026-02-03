# NetApp Console Documentation Guide

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


#### External Link Notation
- **Absolute URLs**: Always include `^` at the end of link text to indicate an external link that opens in a new window
- Pattern: `https://docs.netapp.com/us-en/<path>[Link text^]`
- Example: `https://docs.netapp.com/us-en/console-automation/tenancyv4/overview.html[Learn about the API for NetApp Console IAM^]`
- Internal links (relative paths ending in `.html`) do NOT use `^`


## 5. Common Writer Tasks

### External Documentation Links
- Other NetApp doc sites: `https://docs.netapp.com/us-en/<product>/`
- Always use `^` suffix for external links to open in new window
- Console automation API: `https://docs.netapp.com/us-en/console-automation/`



### Release notes guidelines

 **CRITICAL - Use absolute URLs**: All links and images in whatsnew files MUST use complete absolute URLs (e.g., `https://docs.netapp.com/us-en/console-setup-admin/task-example.html[Link text^]`), not relative paths. This is because whatsnew files are included into the main whats-new.adoc and relative paths will break.




