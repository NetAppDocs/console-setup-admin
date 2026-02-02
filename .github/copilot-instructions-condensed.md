# NetApp Console Documentation Guide (Condensed)

## Product Overview
NetApp Console unifies storage management across on-premises and cloud environments. Documentation uses AsciiDoc format with NetApp Docs Builder toolchain.

## Critical File Naming Rules
**REQUIRED**: All content files MUST start with: `concept-`, `task-`, or `reference-` prefix
Exception: `legal-notices.adoc` only

## Product Terminology (Required)

### Product Name
- Headings: "NetApp Console" (no "the")
- Body text: First use "the NetApp Console", then "the Console"

### Console Agent
- First reference: "Console agent" (capitalize "Console")
- Subsequent: "Console agent" or "agent" (lowercase)
- NEVER use: "Connector", "BlueXP agent", "console agent" (lowercase first word)

### IAM Hierarchy
Always use exact order: Organization → Folders → Projects → Resources
- Resources associate with projects (not folders)
- Roles: platform, application, or data service (specify which)

### Cloud Provider Terms
- AWS: "IAM role ARN" or "access keys for IAM user"
- Azure: "service principal" or "managed identity"
- Google Cloud: "service account"
- Deployment modes: standard mode, restricted mode, private mode (NEVER "offline" or "air-gapped")

## Writing Rules

### Active Voice (Primary)
Subject performs action: "Console agents enable you to..." NOT "Storage is managed by..."
Acceptable passive only for: unknown actor, avoiding blame, prerequisites

### Multi-Cloud Patterns
Check parallel files when updating: `task-adding-{aws|azure|gcp}-accounts.adoc`

## AsciiDoc Patterns

### Front Matter (Required)
```yaml
---
sidebar: sidebar
permalink: filename.html
keywords: comma, separated, keywords
summary: "Brief description"
---
```

### External Links
Always use `^` suffix: `https://example.com[Text^]`
Internal links (`.html`) do NOT use `^`

## Release Notes
Files in `_whatsnew/YYYY-MM-DD.adoc`
**CRITICAL**: Use absolute URLs only (not relative paths) - includes break otherwise
Structure: Console agent section, then NetApp Console administration section

## Agent Best Practices
- Maintain filename-permalink alignment
- Update both `project.yml` sidebar and `_index.yml` for new pages
- Use includes from `_include/` for repeated content
- Validate cross-references and include tag names (case-sensitive)
