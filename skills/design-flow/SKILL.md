---
name: design-flow
description: Apply design constraints to Web/mobile design work and user-facing interface changes; allow template or generated-direction recommendations only for explicit new-page design or existing-page redesign requests.
---

# Design Flow

Use this Skill when the user explicitly asks for web/mobile visual or interaction design, or when user-facing feature work adds or changes visible controls, layout, interaction, or states and must follow the existing design system. A language switcher, filter, form field, or permission entry point added to an existing interface belongs here; backend-only localization, routing, permissions, or data wiring with no rendered-interface impact does not.

Keep recommendation intent separate from design constraints. Template catalogs, generated design directions, and selection cards are allowed only when the user explicitly asks to design a new page or screen, or explicitly asks to redesign an existing page or screen. Feature additions, bounded refinements, and small interaction changes must preserve the established visual authority and take the recommendation-free enhancement branch. Do not infer recommendation intent from words such as page, component, UI, style, image, or CSS.

Do not use it for debugging, diagnosis, code review, API/auth/network/data/state/performance issues, or behavior-preserving fixes. A screenshot or image attached as evidence does not make a task a design task, including bugs involving image preview, upload, or display.

After activation:

1. Use the `Workflow` tool to inspect status and select the route that matches the request.
2. Follow the current step returned by `Workflow`; its required specialist Skills are loaded automatically. Recommendation stages are eligible only on `new-web`/`new-mobile`, or after `existing-web`/`existing-mobile` classifies an explicit redesign with outcome `redesign`. Existing-interface feature additions, bounded refinements, and small interaction changes must use outcome `enhancement`, which skips image capability, generated directions, templates, selection cards, design thesis, and standalone prototype steps. On a recommendation-eligible request, an explicit instruction not to use, recommend, browse, or show templates or generated directions is binding: record it and take the `template-free` transition directly to `direct-thesis`. Otherwise use a callable text-to-image MCP first and fall back to template recommendation only when no qualifying MCP exists, generation fails, or the user skips generated directions; use `DesignSelectCards` for recommendation choices and fall back to `AskUserQuestion` only when cards are unavailable.
3. Complete a manual checkpoint with `Workflow complete_step` and non-empty evidence. Supply `status` or `outcome` when the step declares alternatives.
4. When a card step is active, call `DesignSelectCards`; its select, next, skip, and cancel result advances the workflow automatically.
5. Use the normal auto permission policy throughout the workflow. Store design artifacts below `.ohmyagent/design/` when the active step calls for persisted design evidence.
6. Do not provide a final answer until the workflow reaches `completed` or persistent `cancelled`.
7. For new-page and explicit-redesign branches, `completed` means the prototype passed both the tool-scored `design-jury` and rendered `prototype-quality-gate`; do not start product implementation in that same design round. For an `enhancement` branch, `completed` instead requires direct product implementation plus the rendered enhancement quality gate and build, accessibility, responsive, and state verification. Never invent measurements, reuse pre-fix screenshots, bypass a declared gate, or average a blocker into a passing result.
8. When the user explicitly asks to develop an existing finished prototype, select `implement-web` or `implement-mobile`. Do not use those routes for bounded changes to an existing product; use the matching existing-interface route and its `enhancement` outcome. Ask the user to choose between design and product development only when their intent is materially ambiguous.

The route graph, step instructions, transitions, and write policies are defined solely by `workflow.json`. Specialist Skills remain authoritative for their professional constraints.
