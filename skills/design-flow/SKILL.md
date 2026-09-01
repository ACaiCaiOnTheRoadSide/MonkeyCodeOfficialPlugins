---
name: design-flow
description: Apply design constraints to explicit Web/mobile design work and user-facing interface changes; reserve template or generated-direction recommendations for explicit new-page design or broad redesign.
---

# Design Flow

Use this Skill when the user explicitly asks for Web/mobile visual or interaction design, or when user-facing feature work adds or changes visible controls, layout, interaction, or states and must follow the existing design system. A language switcher, filter, form field, or permission entry point added to an existing interface belongs here; backend-only localization, routing, permissions, or data wiring with no rendered-interface impact does not.

Do not infer design work merely from nouns such as page, component, font, color, image, CSS, or asset when the requested change has no visual or interaction impact. This excludes asset engineering such as embedding, bundling, self-hosting, subsetting, loading, or replacing fonts, images, or other assets unless the user explicitly asks to change or evaluate the visual result.

Keep recommendation intent separate from design constraints. Template catalogs, generated design directions, and selection cards are allowed only for an explicit new page or screen design, or an explicit broad redesign of an existing page or screen. Existing-interface work must be proportional: copy, icon, spacing, and equivalent local changes take `micro`; bounded product features that introduce controls, interactions, layout behavior, or states take `enhancement`; bounded design/prototype improvements take `refine`; and a single new visual thesis without exploration takes `restyle`. None of these four outcomes enters recommendation stages.

Do not use this Skill for debugging, diagnosis, code review, API/auth/network/data/state/performance issues, or behavior-preserving fixes. A screenshot or image attached as evidence does not make a task a design task, including bugs involving image preview, upload, or display.

After activation:

1. Use `Workflow` to inspect status and select the route matching the request.
2. Follow the current step; required specialist Skills load automatically. Recommendation stages are eligible only on `new-web`/`new-mobile`, or after `existing-web`/`existing-mobile` returns `redesign`. Existing-interface outcomes `micro`, `enhancement`, `refine`, and `restyle` skip image capability, generated directions, templates, selection cards, and recommendation stages.
3. On a recommendation-eligible request, an explicit user instruction not to use, recommend, browse, or show templates is binding; the same applies to generated directions. Record it at route entry and take the `template-free` transition directly to `direct-thesis`. Otherwise prefer callable MCP text-to-image generation and fall back to templates only when unavailable, failed, or skipped; use `DesignSelectCards`, then `AskUserQuestion` only when cards are unavailable.
4. Complete manual checkpoints with `Workflow complete_step` and non-empty evidence. Supply the declared `status` or `outcome`. Card tool results advance their steps automatically. When the user's intent and required decisions are already clear, advance required workflow steps autonomously; never pause merely to ask the user to reply “continue”, “可以”, or an equivalent acknowledgement.
5. Follow each step's write policy. Design/prototype and image branches write only below `.ohmyagent/design/`; `micro`, `enhancement`, `implement-web`, and `implement-mobile` product steps may modify product files.
6. Persist a selected generated direction before visual-foundation work; never reconstruct it from memory or a numbered label.
7. Do not provide a final answer until the workflow reaches `completed` or persistent `cancelled`.
8. New-page, redesign, refine, and restyle design branches complete only after the rendered `prototype-quality-gate` passes and then the tool-scored `design-jury` passes. A `micro` branch requires direct implementation and focused checks without screenshots or scoring. An `enhancement` branch requires direct implementation, relevant build checks, representative rendered hard-blocker inspection, and targeted accessibility, responsive, and state verification without a percentage scorecard.
9. Never invent measurements, reuse pre-fix screenshots, bypass a declared gate, self-score the jury, or average a blocker into a passing result.
10. Use `implement-web` or `implement-mobile` to develop an existing relevant prototype. A matching non-empty static prototype is sufficient implementation authority: it need not already behave like the finished product or demonstrate every runtime interaction and state. Implement omitted behavior from the user's request and repository patterns rather than blocking for a more runnable prototype or another approval. Use the matching existing-interface `micro` or `enhancement` outcome for bounded product changes. Ask whether the user wants design or product development only when intent is materially ambiguous.
11. If the user's request already includes both design and implementation, complete the required design evidence and continue into product implementation without asking for a second confirmation. Quality gates may require autonomous corrections, but they must not create an acknowledgement-only user checkpoint.

The route graph, step instructions, transitions, and write policies are defined solely by `workflow.json`. Specialist Skills remain authoritative for their professional constraints.
