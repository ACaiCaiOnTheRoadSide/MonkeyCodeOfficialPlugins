---
name: design-flow
description: Use for explicit web/mobile visual or interaction design work and standalone image creation, editing, or visual evaluation; excludes diagnosis and behavior-preserving fixes.
---

# Design Flow

Use this Skill only when the user's primary intent is to create, redesign, optimize, or evaluate the visual or interaction design of a web/mobile interface, or to create, edit, or visually evaluate standalone image content.

Do not use it for debugging, diagnosis, code review, API/auth/network/data/state/performance issues, or behavior-preserving fixes. A screenshot or image attached as evidence does not make a task a design task, including bugs involving image preview, upload, or display.

After activation:

1. Use the `Workflow` tool to inspect status and select the route that matches the request.
2. Follow the current step returned by `Workflow`; its required specialist Skills are loaded automatically. An explicit user instruction not to use, recommend, browse, or show templates is binding: record it at the route entry and take the `template-free` transition directly to `direct-thesis`, without checking image-generation capability or invoking template catalogs, template artifacts, or selection-card tools. Otherwise, for Web/mobile routes, use a callable text-to-image MCP first and fall back to template recommendation only when no qualifying MCP exists, generation fails, or the user skips generated directions. Prefer `DesignSelectCards`, fall back to `AskUserQuestion` when cards are unavailable, and automatically choose the strongest recommendation when neither interaction tool exists.
3. Complete a manual checkpoint with `Workflow complete_step` and non-empty evidence. Supply `status` or `outcome` when the step declares alternatives.
4. When a card step is active, call `DesignSelectCards`; its select, next, skip, and cancel result advances the workflow automatically.
5. Use the normal auto permission policy throughout the workflow. Store design artifacts below `.ohmyagent/design/` when the active step calls for persisted design evidence.
6. Do not provide a final answer until the workflow reaches `completed` or persistent `cancelled`.
7. For Web and mobile design routes, `completed` means the prototype passed both the tool-scored `design-jury` and the rendered `prototype-quality-gate`, not merely that its HTML opens. Never self-score the jury, bypass either gate, invent measurements, reuse pre-fix screenshots, or average a blocker into a passing total. Present the result and tell the user they can explicitly ask to develop the product or request another design adjustment; do not start product implementation in the same design round.
8. When the user explicitly asks to develop an existing finished prototype, select `implement-web` or `implement-mobile`. When it is materially ambiguous whether they want design work or product development, call `AskUserQuestion` first with a focused choice between continuing design and developing the product, then select the matching route from the user's actual answer. Do not ask when the intent is already clear.

The route graph, step instructions, transitions, and write policies are defined solely by `workflow.json`. Specialist Skills remain authoritative for their professional constraints.
