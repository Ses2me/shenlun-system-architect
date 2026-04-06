# Question-bank ingestion for shenlun systems

## Purpose

Use this reference when the product depends on collecting, importing, cleaning, classifying, and reusing shenlun questions. The goal is to turn messy raw content into a governed question bank that can support grading, recommendation, and controlled generation.

## Supported source patterns

### 1. Public web collection
Typical sources:
- official or semi-official historical question pages
- coaching sites and blogs
- community reposts and exam summaries
- PDF or image scans reposted online

Design concerns:
- copyright and allowed collection scope
- duplicated or conflicting versions
- low-quality OCR or copied text
- missing answer guidance or rubric
- unstable page structure over time

### 2. Manual zip import
Typical payloads:
- word documents
- PDF sets
- spreadsheets
- answer keys
- rubric notes
- scanned images

Design concerns:
- mixed file types in one archive
- inconsistent naming conventions
- partial metadata
- duplicate files across versions
- parsing failures and exception handling

### 3. Internal teaching-research bank
Typical state:
- already partially structured
- hidden taxonomy differences across teams
- multiple answer versions
- inconsistent difficulty labels

Design concerns:
- normalization without losing legacy knowledge
- auditability of changes
- version control for rubrics and exemplars

## Canonical content model

Recommend a normalized schema with at least these entities.

### Question
- question_id
- source_type
- source_reference
- exam_year
- region
- exam_series or paper_name
- question_type
- topic
- prompt_text
- materials_text
- answer_requirements
- word_limit
- difficulty
- status

### Rubric
- rubric_id
- linked_question_type
- scoring_dimensions
- weight_by_dimension
- pass_fail constraints if any
- version
- effective_date

### Reference content
- exemplar_answer
- outline or key points
- official-style interpretation if available
- teaching-research commentary

### Taxonomy and tags
- policy topic
- governance topic
- reasoning pattern
- writing structure tag
- capability tag
- training stage

## Ingestion pipeline

### Stage 1: intake
Capture where the item came from and preserve raw files.

Output:
- raw asset storage key
- source metadata
- initial ingest job id

### Stage 2: extraction
Parse text and fields from input documents or collected pages.

Typical tasks:
- text extraction
- split question stem from materials
- extract year, region, and category
- identify answer instructions
- detect whether exemplar answers exist

### Stage 3: normalization
Transform extracted content into canonical fields.

Typical tasks:
- normalize years and region names
- standardize question type names
- clean formatting noise
- unify punctuation and numbering

### Stage 4: deduplication
Detect duplicates and near-duplicates.

Signals:
- identical prompt or materials
- same year plus region plus topic
- high semantic overlap
- same question with minor formatting changes

### Stage 5: classification
Assign tags and categories.

Possible approaches:
- rules first for explicit metadata
- llm classification for topic and capability tags
- human validation for ambiguous cases

### Stage 6: review and publish
Do not auto-publish all entries.

Use a queue with:
- validation status
- extraction confidence
- missing field flags
- reviewer notes
- publish decision

## Design recommendations

### Recommendation A
If the first release depends on a zip import, design for exception management. Many files will fail clean parsing or contain partial fields.

### Recommendation B
Preserve traceability from every structured question back to the raw source file or page. This is critical for content review and issue resolution.

### Recommendation C
Keep generation downstream from governance. Do not let ai-generated questions enter the same bank as trusted real questions without a separate status and review process.

### Recommendation D
Prefer light adaptation from verified real questions over unconstrained question generation in early releases.

## When the user asks for ai question generation

Recommend a layered strategy:

1. retrieve a real similar question
2. adapt parameters or materials within bounded constraints
3. generate candidate content
4. run policy and quality checks
5. require teaching-research review before publication

## Output pattern for architecture answers

When question-bank design is central, include:
- source landscape
- ingestion workflow
- structured schema
- classification strategy
- review queue design
- publish rules
- reuse paths for grading and recommendation
