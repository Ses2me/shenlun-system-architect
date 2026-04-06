# Evaluation checklist for shenlun ai systems

## Purpose

Use this reference whenever the design includes grading, feedback, recommendation, question generation, or bank ingestion. The product recommendation is incomplete without an evaluation and rollout plan.

## Evaluation layers

### 1. Offline content and parsing evaluation
Use for question-bank ingestion.

Check:
- extraction accuracy for prompt, materials, and metadata
- duplicate-detection quality
- classification accuracy for tags and taxonomy
- publish-queue precision and recall
- import exception rate by file type

### 2. Offline grading evaluation
Use for scoring quality.

Check:
- agreement with senior human graders
- agreement by scoring dimension
- calibration by score band
- consistency across similar answers
- false confidence rate
- review-routing precision

### 3. Offline feedback evaluation
Use for feedback usefulness.

Check:
- actionability
- specificity
- alignment with actual answer weaknesses
- non-generic language rate
- harmful or misleading advice rate

### 4. Recommendation evaluation
Use for learning suggestions.

Check:
- mapping quality from weakness tags to recommended action
- teacher acceptance of recommendation logic
- student uptake of recommended next step
- downstream improvement correlation if available

### 5. Online operational evaluation
Use for rollout.

Check:
- average turnaround time
- reviewer workload change
- auto-pass rate
- dispute rate
- manual override rate
- student satisfaction
- repeat practice rate
- conversion or retention impact if applicable

## Gold-set design suggestions

Create a reference set with:
- diverse regions and years
- multiple question types
- high, middle, and low quality answers
- edge cases such as incomplete or off-topic answers
- disputed examples where human graders debate outcomes

Prefer multiple human labels where possible. Track disagreement rather than hiding it.

## Minimum launch checklist

Before broad release, verify:
- rubric versioning exists
- routing threshold exists
- reviewer console can inspect evidence and edit outcomes
- node outputs are logged for replay
- bad outputs can be rolled back or hidden
- evaluation baseline is documented
- generated questions are clearly separated from trusted real questions

## Warning signs

Flag these as serious risks:
- high confidence on clearly weak outputs
- very polished but empty feedback
- major score swings on near-identical answers
- recommendation logic that ignores the actual scoring evidence
- imported question-bank items published with low extraction confidence

## Output pattern for architecture answers

When evaluation matters, include:
- what to evaluate offline first
- what to measure in pilot launch
- what threshold would block scale-up
- what logs or instrumentation are required
