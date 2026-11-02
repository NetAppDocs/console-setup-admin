# Copilot instructions for NetApp Console documentation

## Repository overview

Product: NetApp Console

NetApp Console is a platform for managing NetApp storage and data services across on-premises and cloud environments, available as a SaaS platform or as a self-hosted deployment in a sovereign cloud or on-premises environment. This documentation covers NetApp Console setup and administration, including deployment modes, Console agents, networking, cloud credentials, and identity and access management.

## Repository structure

- `_include/` - Reusable AsciiDoc content
- `_whatsnew/` - Release-note source content included in `whats-new.adoc`
- `media/` - Images and other documentation media
- `scripts/` - Documentation maintenance scripts
- `store-redirects/` - Redirect definitions for moved or renamed topics

## Product-specific context

- **Product name usage:** Use `NetApp Console` in headings. In body text, use `the NetApp Console` on first reference and `the Console` afterward when the meaning is clear.
- **Console agent:** Use `Console agent` in body prose; use `Console Agent` only for the exact UI label.
- **Deployment modes:** NetApp Console supports standard, restricted, and private modes. State the applicable mode when a capability or procedure is not universal.
- **Console agents:** Console agents connect NetApp Console to storage systems and data services. They can be installed and maintained in AWS, Azure, Google Cloud, or on-premises environments.
- **IAM:** IAM organizes resources through an organization, folders, and projects. Roles assigned at those levels determine member access to resources.

## Typical user workflows

- **Onboard:** Choose a deployment mode → prepare network access → sign up or deploy a Console agent → subscribe to services
- **Administer agents:** Install or maintain an agent → configure connectivity or proxy settings → associate with projects → troubleshoot or upgrade
- **Manage access:** Set up the organization, folders, and projects → add members → assign roles → associate resources
- **Connect cloud resources:** Configure provider-specific credentials and permissions → add or manage cloud resources
