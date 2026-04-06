# Grading workflows for shenlun essay products

## Purpose

Use this reference to design production-oriented workflows for shenlun grading. Default to ai first-pass plus human review unless the user explicitly accepts lower reliability.

## Why shenlun grading is not a single prompt

A production system must separate:
- answer understanding
- rubric selection
- dimension scoring
- evidence capture
- final score aggregation
- narrative feedback
- recommendation generation
- human review routing

This separation improves auditability, consistency, and operational control.

## Baseline workflow

### Node 1: answer intake and normalization
Input:
- question id or full prompt
- materials
- candidate answer
- user identity or attempt context

Output:
- clean answer text
- answer length
- segmentation if needed
- anomaly flags

Prefer rules and preprocessing over llm here.

### Node 2: question recognition and rubric binding
Goal:
Bind the correct rubric or scoring template to the answer.

Input:
- question metadata
- taxonomy
- exam type

Output:
- selected rubric version
- scoring dimensions
- weight settings

Use rules first. Use llm only when metadata is incomplete.

### Node 3: structural and compliance checks
Possible checks:
- empty or severely incomplete response
- word-count mismatch
- forbidden formatting patterns
- obvious off-topic signals

This node can short-circuit later steps or trigger special handling.

### Node 4: dimension-level scoring with evidence
Typical scoring dimensions:
- relevance to question intent
- structure and organization
- use of provided materials
- argument quality or reasoning
- expression and language quality

Required output per dimension:
- provisional score or band
- short rationale
- supporting evidence span or quoted basis
- confidence estimate

This node is the core llm node.

### Node 5: score aggregation and confidence decision
Goal:
Turn dimension outputs into a provisional total and determine whether the result can pass automatically.

Output:
- total score or grade band
- confidence score
- review recommendation

Do not let this node overwrite evidence-based dimension outputs.

### Node 6: narrative feedback generation
Generate student-facing feedback that is clear and actionable.

Recommended sections:
- overall diagnosis
- strengths
- biggest issues
- revision advice
- next practice focus

Keep this node independent from scoring logic when possible.

### Node 7: learning-tag extraction and recommendation
Map grading results into training insights.

Possible tags:
- weak structure
- weak material usage
- topic drift risk
- generic expression
- poor policy interpretation

Possible outputs:
- next practice set
- targeted micro-lessons
- revision exercises
- teacher follow-up suggestion

### Node 8: human review routing
Route cases into review when:
- confidence is below threshold
- large scoring variance appears across retry runs or models
- content is unusual or high stakes
- user disputes the outcome
- the answer belongs to premium service tiers

### Node 9: storage, analytics, and replay
Persist:
- rubric version
- node outputs
- confidence
- review action
- final accepted result
- recommendation tags

This supports debugging, analytics, and future evaluation.

## Human-in-the-loop policy suggestions

### Strong review mode
Use when:
- premium tutoring
- mock exams with reputational risk
- new rubric rollout
- weak confidence in model stability

Pattern:
AI first-pass → reviewer adjusts or confirms → final release

### Sampled review mode
Use when:
- large-scale daily practice
- moderate reliability requirement
- budget pressure exists

Pattern:
AI final for most cases + targeted sample review + dispute escalation

### Minimal review mode
Use when:
- early internal prototype
- low-stakes self-practice

Pattern:
AI feedback first, final scoring shown as reference only

## Anti-patterns

Do not recommend these without explicit tradeoff notes:
- single-prompt scoring and feedback with no evidence trace
- unconstrained final score without rubric binding
- auto-publication of generated feedback templates with no quality checks
- pure ai grading for premium or high-stakes scenarios in version one

## Output pattern for architecture answers

When grading workflow is central, provide:
- node-by-node workflow
- node objective
- input and output
- suggested implementation mode: rules, llm, retrieval, human
- routing rules
- operational risk notes
