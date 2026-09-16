# Copilot instructions for NetApp Console documentation

## Repository overview

Product: NetApp Console

NetApp Console provides storage management, data protection, and related data services across on-premises and cloud environments. It is available as a SaaS platform or as a self-hosted deployment in a sovereign cloud or on-premises environment, managed through a web console and APIs.

This repository documents NetApp Console setup and administration, including deployment modes, Console agents, networking, cloud credentials, and identity and access management for NetApp Console administrators.

## Repository structure

Most documentation pages are in the repository root. Supporting directories include:

- `_include/` - Reusable AsciiDoc content
- `_whatsnew/` - Release-note source content included in `whats-new.adoc`
- `media/` - Images and other documentation media
- `scripts/` - Documentation maintenance scripts
- `store-redirects/` - Redirect definitions for moved or renamed topics

`project.yml` defines site settings and navigation. Update it or the index files only when a task requires a site-configuration or navigation change.

## Product-specific context

- Use `NetApp Console` in headings. In body text, use `the NetApp Console` on first reference and `the Console` afterward when the meaning is clear.
- Use `Console agent` in body prose; use `Console Agent` only for the exact UI label.
- NetApp Console supports standard, restricted, and private modes. State the applicable mode when a capability or procedure is not universal.
- Console agents connect NetApp Console to storage systems and data services. They can be installed and maintained in AWS, Azure, Google Cloud, or on-premises environments.
- IAM organizes resources through an organization, folders, and projects. Roles assigned at those levels determine member access to resources.
- Keep AWS, Azure, and Google Cloud requirements separate because permissions, credentials, ports, and deployment procedures can differ.
- Preserve established terminology and verify product behavior against nearby repository content. Do not invent permissions, commands, UI labels, or mode support.

## Typical user workflows

Use these workflows when they help determine content scope or task order:

- **Onboard:** Choose a deployment mode, prepare network access, sign up or deploy a Console agent, and subscribe to services as applicable.
- **Administer agents:** Install or maintain an agent, configure connectivity or proxy settings, associate it with projects, and troubleshoot or upgrade it.
- **Manage access:** Set up the organization, folders, and projects, then add members, assign roles, and associate resources.
- **Connect cloud resources:** Configure provider-specific credentials and permissions before adding or managing cloud resources.
