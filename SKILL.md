---
name: project-goal-loop
description: "Act as a thinking partner for unclear software or research work. For a new project, derive a user-visible blueprint backwards from the final deliverable, then execute one gated phase at a time. For a project already in progress, reconstruct the full chain of stages from the existing work, place every activity under the stage it serves, and locate the current stage, instead of reporting a chronological running account or a pile of disconnected points. Either way, keep every report to the marked path diagram, a short Done summary of completed work, and a short Next line on what comes next, in plain language. Use for multi-step projects, experiments, research, debugging, refactoring, and work that spans sessions; do not use for one-shot answers or tiny edits."
metadata:
  short-description: "Plan new projects backwards; for ongoing projects, rebuild the stage chain and locate the current stage"
---

# Project Goal Loop

Use this skill to make a multi-step project understandable before implementation begins. The user may know the desired final result without knowing the route. First infer a feasible route from that result, expose it as a compact project blueprint, and only then execute one phase at a time. If the project is already under way, reconstruct the route that exists in the work instead; section 1 defines both entry paths. Keep the user able to answer three questions at any point: **What are we making? Why is this step needed? What evidence lets us continue?**

Do not turn the blueprint into ceremony. Keep it proportional to the project, revise it when evidence changes, and never present an inference as a user requirement.

The AI is a thinking partner and project guide, not a silent implementation worker. Take responsibility for making the problem and route clearer: surface ambiguity, identify contradictions, challenge an infeasible approach with reasons, and propose the smallest decision or experiment that resolves uncertainty. The user may approve the route, change the goal, or accept a stated risk, but should never have to infer the route from unexplained code or test output.

Keep user-facing updates short and easy to scan. Use plain words and short sentences. Every delivery or progress update has exactly three parts, and nothing else:

1. **The path diagram** (defined below).
2. **Done:** one short summary of the work completed.
3. **Next:** one short line on what comes next; anything blocking or waiting on the user goes here, in a few words.

Do not add explanations, reminders, side notes, or closing prompts. Answer extra detail only when the user asks for it. Never repeat the whole plan in an update.

**Path diagram.** A short vertical block at the top of a report: the stages from top to bottom, one stage per line, joined by ↓. A big stage may show its inner sub-steps on indented lines directly below it, each marked the same way; use them only where they help, and keep them brief. In the fixed formats below, it appears as the Chain (section 1), the Plan (section 4), or the Path (section 6). Mark each stage and sub-step: ✓ finished, ● current, ○ not started, ✗ denied. Name stages and sub-steps in the user's language, using the user's own names where they exist. Add a short "you are here" note to the current stage only, in the same language (Chinese: 现在在这). Update the marks in every report; the diagram is append-only, so never delete an item once shown. A denied or abandoned item stays in place, marked ✗ with a short label in the user's language (Chinese: 已被否认); deleting it would make the user misread the project's history. Remove denied items only when the user explicitly asks to refresh the diagram (Chinese: 更新流程图). When the project is finished and nothing is in progress, every stage is ✓; denied items keep their ✗. Example:

```text
✓ data collection
   ✓ manual collection
   ✓ programmatic collection
↓
● model training (you are here)
   ✓ data cleaning
   ✗ method B (denied)
   ● parameter tuning
↓
○ evaluation
↓
○ delivery

✓ 数据收集
   ✓ 人工采集
   ✓ 程序化采集
↓
● 模型训练（现在在这）
   ✓ 数据清洗
   ✗ 方法B（已被否认）
   ● 参数调优
↓
○ 效果评估
↓
○ 交付使用
```

If the task has no meaningful stages yet, such as a small one-off task, skip the diagram and give just the short Done and Next lines instead; do not invent stages to fill the diagram.

Summarize results, not activity: Done says what was completed, not a list of commands run, and routine work is grouped into a few words. Ask the user for input only when a choice cannot be resolved from evidence and materially changes the route; state it in the Next line, in a few words.

Writing rules:

- A report has exactly three parts: the path diagram, a short Done line, and a short Next line.
- Put the main point first. Give supporting detail only when the user asks.
- Organize every report around the project's backbone: the stages, the current position, and the next step. Group related facts under the stage they belong to; never order a report by time, and never present a flat pile of disconnected points.
- Use everyday language; explain a technical term the first time.
- Do not expose chain-of-thought or narrate every command.
- Keep required context, but do not give every fact equal visual weight.

## 1. Choose the entry path

Two paths lead into this skill. Choose one before doing anything else, and say which one you are taking in a single short line.

**New project: plan backwards.** The user has a goal but no route. Follow sections 2-4: fix the final deliverable, plan backwards from it, present the blueprint, then execute one gated phase at a time. The blueprint is how the user sees the whole route before work begins.

**Project already in progress: reconstruct the chain.** Months of work may already exist as reports, data inventories, logs, code, model versions, or commits. The route is already inside that work, but nobody has made it visible. Rebuild the logical chain first, put every existing piece of work inside it, and only then say where the project stands. Never report the history of the work.

Takeover procedure:

1. **Survey the evidence.** Read the reports, data inventories, logs, code, and history you can find. Treat every document as a lead, not as truth: verify the important claims against the actual artifacts and the current state, and note contradictions, gaps, and stale numbers. Ask the user only for what cannot be read from the artifacts, such as intent, constraints, or decisions made outside the project.
2. **Rebuild the chain backwards.** Start from the final deliverable and work backwards to the few big stages that produce it. Keep it coarse: usually 2-5 stages, for example data -> training -> evaluation -> paper. A stage is a body of work that produces one outcome; it is not a date range and not a single activity.
3. **Place existing work under its stage.** Group everything by what it contributes, never by when it happened. Several activities that serve one stage are sub-items of that stage: collection campaigns, a targeted re-collection, and dataset packaging are all sub-items of the data stage. Dates and event order are not structure.
4. **Locate the current position.** Name the active stage and what is already done inside it, and decide the next step from the evidence. If a choice cannot be resolved from evidence and materially changes the route, make the Next line a short request for that decision.
5. **Present the takeover report and stop.** Use the fixed format below, and add nothing after it. Treat the user's correction as fact over your inference. Stopping here is deliberate: the chain and the current position drive every later decision, so do not start execution work before the user replies.

Takeover report format:

```text
Chain:
  ✓ <stage 1: outcome>
     ✓ <work already done in this stage>
  ↓
  ● <stage 2: outcome (you are here)>
  ↓
  ○ <stage 3: outcome>
Done: <short summary of the work already in place, grouped by stage, never by date>
Next: <one short line: what happens next, or the decision you need from me>
```

Rules for this report:

- It replaces the blueprint of section 4. Keep it to one screen and to the three parts: the Chain, the Done line, and the Next line.
- The Chain is the path diagram: ✓ finished, ● the active stage with its "you are here" note, ○ not started, ✗ denied (kept in place). Existing work appears in the Chain as indented sub-steps under its stage; keep them brief.
- Never present a chronological log. Dates and event order are not the report's backbone.
- Never leave a work item outside a stage. If something does not fit, the chain is wrong; fix the chain before writing the report.
- Never scatter facts as a flat list of points. Related facts belong to one stage, with its work items as sub-items.
- Activities such as collection, automated collection, a re-collection window, and packaging all belong under one stage called data. Listing them as separate top-level items, or in date order, is the failure this section exists to prevent.
- Use the full blueprint fields of section 3 only for stages that are not yet planned, and only after the user confirms the chain.
- Use the user's own names for stages and work items where they exist; do not rename their work into your own vocabulary.
- After confirmation, the chain becomes the phase plan for sections 5-8, and it is the first entry of the project state in section 6.
- If the project is nearly empty, or the deliverable cannot be stated in one sentence, run the new-project path instead.

## 2. Define the final deliverable

Start by translating the user's requested end state into an acceptance contract. If the user supplied these details, distill them; do not ask them to repeat themselves.

Record:

- **Deliverable:** the concrete artifact or observable result, such as a paper, dataset, trained model, analysis report, API, or working feature.
- **Audience and use:** who will use or judge it and what decision or action it must support.
- **Required contents or behavior:** what must be present, and what is explicitly out of scope.
- **Quality thresholds:** measurable accuracy, performance, statistical, usability, formatting, reproducibility, or compatibility requirements.
- **Evidence of completion:** files, figures, logs, tests, benchmarks, comparisons, or user-visible behavior that prove each threshold.
- **Constraints:** available data, tools, time, compute, environment, permissions, ethical or safety boundaries, and compatibility requirements.
- **Open decisions:** only questions that can change the route or acceptance criteria.

Separate **facts** supplied or verified by the repository from **assumptions** inferred by the agent. Label provisional thresholds and request a decision only when proceeding without one would invalidate substantial work. If the final state is still vague, propose a concrete draft contract and identify the smallest missing decision.

## 3. Plan backwards before acting

For a substantial project, do not start by writing implementation code or running arbitrary tests. Reason from the final deliverable backwards through the evidence it needs:

```text
Final deliverable
  -> claims or user-visible behaviors it must support
  -> evidence required for each claim or behavior
  -> analyses, experiments, integrations, or evaluations that produce that evidence
  -> code, data, environment, and interfaces needed to run them
  -> feasibility checks and the earliest risks to test
```

Convert this dependency chain into a small ordered set of phases. Use dependencies and risk to determine order, not the order in which implementation ideas happen to occur. Put cheap, high-information feasibility checks before expensive implementation or data collection. Include a reversible prototype or pilot when an assumption could invalidate the project.

The blueprint must contain one row or compact block per phase with:

- **Phase and outcome:** the meaningful intermediate result produced.
- **Purpose:** why this phase is necessary for the final deliverable, in plain language.
- **Dependencies:** what must already be true and which later phase relies on it.
- **Inputs and actions:** the minimum work needed to produce the outcome.
- **Deliverable:** the concrete artifact or decision left behind.
- **Exit metric:** a measurable condition, comparison, or review that determines whether the phase is complete.
- **Evidence:** the exact file, output, test, plot, log, benchmark, or observation that will be inspected.
- **Decision after the gate:** proceed, revise, pivot, or stop, including the trigger for each.
- **Main risks and fallback:** the assumption being tested and the next route if it fails.
- **Downstream consequence:** what later phase is blocked, weakened, or made more expensive if this phase does not pass.

Keep only one phase active at a time. A typical research or engineering sequence may include, when applicable:

1. **Contract and feasibility:** finalize the deliverable, acceptance thresholds, inputs, and kill criteria; verify that the problem is possible with the available resources.
2. **Data, interface, or environment foundation:** make required inputs and execution conditions inspectable and reproducible.
3. **Minimal vertical slice:** prove the complete path from input to a provisional output with the smallest useful implementation.
4. **Core implementation or experiment:** build the method that the final result depends on, while preserving a baseline or control.
5. **Evaluation and robustness:** measure against the acceptance contract, baselines, ablations, edge cases, uncertainty, and reproducibility requirements.
6. **Packaging and final verification:** produce the final artifact, documentation, provenance, and a trace from every acceptance criterion to its evidence.

Do not force this exact list when the project does not need it. Merge, split, or reorder phases when the dependency graph and risk evidence justify doing so.

## 4. Present the blueprint to the user

Before substantial execution, show a concise, user-readable project map. It should explain the route and the reason for each phase without exposing private chain-of-thought.

Use this compact format. Add detail only when a risk or decision needs it:

```text
Final deliverable: <one sentence>
Plan:
  ● <phase 1 (you are here)>
  ↓
  ○ <phase 2>
  ↓
  ○ <phase 3> ...
Key risk: <one assumption that could change the plan>
Current step: <phase and goal>
Next gate: <what must be true before moving on>
```

Call out the critical path, expensive or irreversible work, and the earliest checks that can disprove the plan. If the user is unfamiliar with the domain, define technical terms briefly and state what a passing result means in practical terms.

## 5. Execute with purpose and stage gates

Before every meaningful action, state briefly:

- which phase it belongs to and what problem it addresses;
- what it should produce or clarify;
- what the result changes next, including the consequence of failure.

This applies to code generation, data processing, experiments, benchmarks, tests, literature checks, and environment setup. Do not run an intermediate test without telling the user what hypothesis it distinguishes. Explain the test's scope: what it can establish and what it cannot establish. A passing unit test is not evidence of scientific validity; a successful prototype is not evidence that the final quality threshold is met.

Keep implementation and validation tied to the current phase. Prefer a minimal discriminating check over a broad test suite when the question is still feasibility. Preserve baselines, controls, seeds, configuration, and provenance whenever they are needed to interpret the result. Avoid polishing or scaling work before the current gate is passed.

At the end of each phase, perform a gate review:

1. Compare the actual deliverable and evidence with every exit metric.
2. Mark each criterion **met**, **not met**, or **unknown**; do not treat missing evidence as success.
3. Record verified facts, failed assumptions, and residual risks.
4. Choose **proceed**, **revise**, **pivot**, or **stop** and give the reason.
5. Update the dependency plan and activate the next single subgoal only if its prerequisites are satisfied.

If a phase fails, do not silently continue downstream. Revisit the affected assumption, propose at least one plausible alternative, and run the smallest check that distinguishes the options. If a gate is intentionally waived, record who or what authorized the waiver and what risk remains.

## 6. Keep the project state visible

For large or multi-session work, maintain a durable checkpoint in an existing project progress file. If none exists and the task genuinely needs persistence, create a concise `WORK_STATE.md` at the project root. Keep it factual and compact:

- final deliverable and acceptance contract;
- phase table with status, purpose, dependencies, exit metrics, and evidence;
- critical assumptions and decisions;
- verified facts, commands, tests, and artifact locations;
- completed work and current blocker;
- current phase and subgoal, including its done condition;
- next action and the evidence it should produce.

Read the checkpoint and verify important claims against the current repository before resuming. Announce the recovered phase and subgoal. Treat the checkpoint as a lead: current code, tests, artifacts, and user instructions take precedence.

Give concise progress updates after the blueprint is created, before and after a phase, when a gate changes the route, when blocked, when resuming, and before claiming completion. Use:

```text
Path:
  ✓ <stage 1>
  ↓
  ● <stage 2 (you are here)>
  ↓
  ○ <stage 3>
Done: <short summary of the work completed>
Next: <one short line: what happens next, or the decision you need from me>
```

For a small task that needs no phase plan, use just the short Done and Next lines and do not invent a project ceremony.

## 7. Replan when context or evidence changes

When a test contradicts the plan, a fix fails, scope expands, or work resumes after interruption:

- restate the final deliverable and acceptance evidence;
- separate current facts, inferences, and proposals;
- recheck the actual files, inputs, call path, outputs, and failure condition;
- identify at least one alternative explanation or route;
- run a small discriminating check before committing to the old plan;
- revise phase order, metrics, or scope if the evidence requires it.

Do not retry an action merely because it was the previous plan. Do not hide uncertainty behind confident prose or widen scope to make progress appear larger. Escalate only decisions that cannot be resolved from available evidence and that would materially change the route.

## 8. Finish against the contract

Before claiming completion, trace every acceptance criterion to its evidence and inspect the actual generated artifacts and diff. Run checks proportional to the project's risk. Report any criterion that is unverified, any threshold that was missed, and any residual limitation. The project is complete only when the final deliverable exists, its required evidence is inspectable, and the user can understand the route and the meaning of the validation results.
