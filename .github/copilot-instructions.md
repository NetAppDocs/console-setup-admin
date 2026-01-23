# NetApp Console Documentation Codebase Guide

## Project Overview
This is a **documentation-only repository** for NetApp Console setup and administration. It uses **AsciiDoc** format with a structured content management system (likely NetApp Docs Builder or similar toolchain) that generates web documentation from YAML configuration and `.adoc` files.

## Architecture & Structure

### Content Organization
- **concept-*.adoc**: Conceptual overview topics explaining "what" and "why"
- **task-*.adoc**: Procedural how-to guides with step-by-step instructions
- **reference-*.adoc**: Technical reference material (permissions, ports, configurations, IAM roles)
- **_include/**: Reusable content snippets using AsciiDoc tag-based includes
- **_index.yml**: Landing page configuration with tiles and quick links
- **project.yml**: Main sidebar navigation structure and site settings

### Key Components
1. **Sidebar Navigation** ([project.yml](project.yml)): Hierarchical navigation tree with titles and URLs
2. **Content Reuse System** ([_include/](\_include/)): Tagged snippets included via `include::_include/filename.adoc[tag=tagname]`
3. **Media Assets** ([media/](media/)): Screenshots and images referenced as `image::filename.png[]`

## File Naming Conventions

| Prefix | Purpose | Example |
|--------|---------|---------|
| `concept-` | Explain architecture, features, deployment modes | `concept-agents.adoc`, `concept-iam-rbac.adoc` |
| `task-` | Step-by-step procedures | `task-adding-aws-accounts.adoc`, `task-federation-saml.adoc` |
| `reference-` | Technical specifications, permissions, roles | `reference-permissions-aws.adoc`, `reference-iam-platform-roles.adoc` |

## AsciiDoc Patterns in Use

### Standard Frontmatter
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

### Common Markup Conventions
- **Lead paragraph**: `[.lead]` before first paragraph for emphasis
- **Admonitions**: `NOTE:`, `TIP:`, `IMPORTANT:`, `WARNING:`, `CAUTION:` (colon required)
- **Code blocks**: Fenced with `[source,<lang>]` and `----` delimiters
- **Tables**: Use `[cols=N*,options="header"]` or `[cols="width,width"]` syntax
- **Cross-references**: `link:other-page.html[Link text]` for internal docs
- **External links**: Add `^` for new window: `https://example.com[Text^]`

### Include Pattern (Critical for DRY)
Shared content lives in `_include/` with tagged regions:
```asciidoc
// In _include/tasks-role.adoc
//tag::add-role[]
Step-by-step content here
//end::add-role[]

// In consuming file
include::_include/tasks-role.adoc[tag=add-role]
```

## Content Structure Guidelines

### Task Files Structure
1. Title and frontmatter
2. `[.lead]` summary paragraph
3. **Overview** section (when applicable)
4. **Prerequisites** (as `.Before you begin` or bullet list)
5. **Steps** with numbered procedures
6. **Result** or **What's next** sections

### Reference Files Structure
- Permission files contain JSON/YAML policy documents in code blocks
- IAM role references use tables with columns: Role | Description | Permissions
- Port/networking references use tables with: Port | Protocol | Direction | Purpose

## Multi-Cloud Provider Patterns
Files are often duplicated across AWS, Azure, and Google Cloud with parallel structures:
- `task-adding-{aws|azure|gcp}-accounts.adoc`
- `reference-permissions-{aws|azure|gcp}.adoc`
- `reference-ports-{aws|azure|gcp}.adoc`

When updating cloud provider documentation, check if parallel files need similar updates.

## Integration Points

### External Documentation Links
- Other NetApp doc sites: `https://docs.netapp.com/us-en/<product>/`
- Always use `^` suffix for external links to open in new window
- Console automation API: `https://docs.netapp.com/us-en/console-automation/`

### Release Notes Integration
- **release_notes_autogen** in [project.yml](project.yml) links to `console-relnotes` repo
- Auto-generates "What's new" content from separate release notes repository

## Development Workflow

### Building Documentation
This repo uses NetApp's documentation build system (not included in repo). Builds are triggered via CI/CD when pushed to remote.

**No local build process**: Preview by pushing to a branch or use NetApp internal tools.

### Testing Changes
1. Validate AsciiDoc syntax (use AsciiDoc extension for VS Code)
2. Check cross-references resolve correctly
3. Verify include directives reference existing tagged regions
4. Ensure new pages are added to [project.yml](project.yml) sidebar

### Navigation Updates
When adding new pages, update **both**:
1. [project.yml](project.yml) - Add to `sidebar.entries` hierarchy
2. [_index.yml](_index.yml) - Add to landing page tiles if it's a top-level topic

## Common Gotchas

1. **Permalink must match filename**: `permalink: task-example.html` for `task-example.adoc`
2. **Include tags case-sensitive**: `tag::add-role[]` not `tag::add-Role[]`
3. **Admonition syntax**: Must end with `:` → `NOTE:` works, `NOTE` doesn't
4. **Image paths**: Set via `:imagesdir: ./media/` then reference as `image::file.png[]`
5. **Table formatting**: Headers require `options="header"` or use `[cols=3*,options="header"]`

## Critical Files

- [project.yml](project.yml): Site configuration and complete navigation tree
- [_index.yml](_index.yml): Landing page layout with topic tiles
- [concept-overview.adoc](concept-overview.adoc): Main product overview, often referenced
- [concept-identity-and-access-management.adoc](concept-identity-and-access-management.adoc): Core IAM concepts
- [_include/endpoints-agent.adoc](_include/endpoints-agent.adoc): Reused networking requirements across multiple pages

## AI Agent Best Practices

1. **Always check frontmatter**: Ensure `permalink`, `keywords`, and `summary` are present and accurate
2. **Maintain filename-permalink alignment**: File `task-example.adoc` → `permalink: task-example.html`
3. **Use includes for repeated content**: Don't duplicate steps; create tagged includes in `_include/`
4. **Update navigation**: New pages require entries in [project.yml](project.yml)
5. **Follow cloud provider patterns**: When adding AWS content, consider if Azure/GCP equivalents are needed
6. **Validate links**: Internal links use `.html` extension, external links need `^` for new window
7. **Respect heading hierarchy**: Level 1 (`=`) for title only, content starts at level 2 (`==`)
