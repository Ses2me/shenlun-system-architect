# Shenlun System Architect

A product-design skill for AI-enabled **申论题库、批改、反馈与训练系统**.  
It helps product managers turn messy business ideas into **system architecture, workflow/agent design, evaluation plans, and MVP rollout paths**.

## What this skill does

This skill is designed for **product managers**, not end learners.

It analyzes 公考申论场景 and outputs a structured solution for:

- question bank ingestion and governance
- web-collected or manually uploaded real-question libraries
- question classification and structured metadata design
- AI first-pass grading + human review workflows
- feedback generation and learning recommendation chains
- workflow / agent node design
- backend configuration and operations support
- evaluation metrics, review loops, and rollout strategy

## Best use cases

Use this skill when you need to design products such as:

- AI 申论批改系统
- 申论 AI 初评 + 人工复核平台
- 公考主观题反馈与训练系统
- 真题库导入、分类、治理与出题系统
- 基于真题的轻改编出题与训练链路
- 申论批改后台、质检后台、运营配置后台

## What makes it different

This is **not** a generic PRD generator.

It is built around several product-level design principles:

1. **Do not treat grading as a single model call**
   - split grading into structured nodes
   - separate scoring, explanation, feedback, and recommendation

2. **Prefer AI first-pass + human review**
   - especially for high-stakes subjective assessment
   - support confidence thresholds and dispute routing

3. **Treat question-bank governance as a first-class system**
   - question ingestion, parsing, classification, deduplication, and review
   - not just “upload files and start grading”

4. **Design for evaluation and operations**
   - consistency checks
   - review sampling
   - backend configurability
   - online quality monitoring

## Typical input

You can prompt the skill with requests like:

- Design an AI 申论批改 system for a 公考 platform
- Help me design AI first-pass grading plus human review for subjective answers
- Build a workflow for ingesting real exam questions from uploaded zip files
- Design a backend for 申论 rubric configuration and review thresholds
- Create an MVP architecture for question bank + grading + feedback + recommendation

## Typical output

The skill usually produces a structured design with sections such as:

1. business goal and scenario definition
2. question bank source and ingestion design
3. classification and structured metadata strategy
4. grading task decomposition
5. AI / rules / human division of labor
6. system architecture and workflow nodes
7. feedback and learning recommendation chain
8. backend configuration and operations design
9. evaluation metrics and validation plan
10. MVP and iteration roadmap

## Recommended usage pattern

For best results, provide:

- target users
- product goal
- current manual workflow
- question source
- review requirements
- expected accuracy / consistency level
- whether this is MVP or platform-scale design

The more constraints you provide, the more differentiated the output becomes.

## Example prompts

### 1. AI grading platform
Design a 公考申论 AI grading system.  
Goal: improve grading efficiency while keeping score consistency acceptable.  
Mode: AI first-pass + human review.  
Please output system architecture, workflow nodes, backend configuration, and evaluation plan.

### 2. Question-bank ingestion
We have a zip file of real exam questions, sample answers, and rubrics.  
Design a product workflow for ingestion, parsing, classification, metadata extraction, review, and downstream reuse for grading and training.

### 3. Training and recommendation
Design a learning workflow where grading results are converted into weakness tags, personalized feedback, and follow-up practice recommendations for 申论 learners.

## Repository structure

```text
SKILL.md
agents/
  openai.yaml
references/
  question-bank-ingestion.md
  grading-workflows.md
  evaluation-checklist.md
