---
name: user-focused-examples
description: "Create or revise two short, imperative, user-focused purpose statements for NetApp documentation. Use when writing a use-case paragraph, user-focused example, contextual task introduction, or reusable concept and task content. Ground statements in documented behavior and relevant personas; do not write UI steps."
argument-hint: "Target page, existing text, capability, user goal, or placement"
user-invocable: true
---

# User-Focused Examples

Create or revise two concise imperative alternatives that state the user's goal and why it matters. These purpose statements give task and concept pages reusable, outcome-focused context. They do not instruct the user how to complete a task.

## Inputs

Request the target page, existing text to revise, capability, user goal, or intended placement when it is not available in the conversation. Valid placements are a task lead, text before a procedure, or a concept introduction. Read the target page and the related documentation that verifies the product behavior before drafting.

Use the personas in [Persona guidance](./references/personas.md) to select a credible user context. Use [Use-case guidance](./references/use-case-guidance.md) to distinguish a use case from a feature description or procedure. Consult [Examples](./references/examples.md) for the expected output shape. For requests involving ONTAP concepts, consult [ONTAP guidance](./references/ontap-guide.md).

## Workflow

1. Identify the documented capability, the user goal it supports, and why that goal matters.
2. Select a relevant persona to understand the user's context, but do not name the persona in the statement unless the writer asks.
3. Compare the draft with the target page's lead and nearby content. Identify the missing user goal; do not restate existing feature descriptions, outcomes, or task instructions.
4. Draft two materially different alternatives. Each alternative should be one imperative sentence of 12 to 25 words.
5. If revising existing text, preserve the verified meaning while replacing feature-focused or procedural wording with a concise imperative goal and outcome.
6. For ONTAP concepts not verified by the target page or related repository content, use the ONTAP guidance to retrieve only the narrowest canonical source needed to verify terminology or behavior.
7. State any uncertainty or unsupported outcome rather than inventing behavior, customer results, or product details.

## Required Style

- Start with an imperative verb that expresses the user's goal, such as "Investigate," "Determine," "Protect," "Maintain," or "Identify."
- Use active voice and direct, user-focused language.
- Write in a neutral documentation tone, not marketing language.
- Follow the use-case formula in imperative form: action, concrete problem, and documented operational consequence.
- Lead with the user's goal or problem, not the product, feature name, or persona.
- Use a concrete operational consequence supported by the documentation, such as preventing service disruption, maintaining compliance, or isolating a performance issue.
- Mention only the documented capability needed to connect the user problem to the page; do not turn the example into a feature summary.
- Avoid generic claims such as "easy," "seamless," "efficient," "streamlined," or "powerful" unless the source documentation establishes a specific outcome.
- Make each paragraph understandable when read outside its original page.
- Refer to the product name required by the target repository's instructions.
- Make the two alternatives distinct, such as by using different priorities, operational pressures, or valid persona contexts.

## Prohibited Content

- Do not include UI navigation, UI labels, selections, field names, commands, numbered actions, or procedural instructions.
- Do not use action-sequencing language such as "first," "then," "next," "select," "click," or "enter."
- Do not restate detailed task steps, list feature capabilities, or make generic value claims.
- Do not repeat the target page's lead or nearby content with minor word changes.
- Do not invent product behavior, metrics, customer outcomes, persona details, or prerequisites.
- Do not infer ONTAP behavior from general knowledge or claim that NetApp Console (local deployment) supports an ONTAP capability unless repository content documents that integration.

## Final Check

Before responding, verify that each paragraph:

- Starts with an imperative verb and states a user goal and why it matters.
- Is supported by the target page or related documentation.
- Adds user motivation that is absent from the target page rather than rephrasing its lead.
- Is one sentence and 12 to 25 words, unless the writer requested a different length.
- Contains no UI or procedural language.
- Can be reused in a related concept or task page without relying on nearby steps.

Return only the two alternatives by default. Provide source pages, persona context, or placement rationale only when the writer requests it.