# FormEvolve-AI: Multimodal Form Parser with Prompt Self-Evolution Loop

An end-to-end framework leveraging **Gemini 2.5 Flash** and **Structured Outputs** to extract structured key-value data directly from complex scanned document forms (FUNSD Dataset) without traditional OCR pipelines. The system features an automated **Prompt Self-Correction & Evolution Loop** that continuously refines AI instructions until target accuracy is achieved.

## Key Features

- **End-to-End Multimodal Parsing**: Skips traditional two-step pipelines (OCR text extraction followed by NLP text parsing). Gemini directly processes document images to extract structural layout and semantic meaning simultaneously.
- **Enforced JSON Schemas**: Utilizes Pydantic to strictly enforce structured data output (`ExtractedForm`), ensuring reliable integration into downstream business applications.
- **Automated Python Grader**: Integrates an objective evaluation function that automatically maps and grades AI output against the official FUNSD ground-truth relationships.
- **Self-Correcting "Judge-Worker" Loop**: When extraction accuracy falls below the target threshold, a meta-cognitive Judge LLM analyzes the grader's error logs and auto-rewrites more advanced spatial and alignment constraints into the prompt for the next generation.

## System Architecture

The pipeline consists of three core AI-driven agent personas collaborating iteratively:

1. **The Worker (Gemini 2.5 Flash)**: Acts as the data extractor. It views the image, applies the current prompt instructions, and outputs key-value pairs matching the target JSON schema.
2. **The Grader (Python Evaluation Function)**: Acts as the strict exam evaluator. It automatically maps the Worker's JSON against ground truth linking annotations, calculates the exact matching percentage, and identifies missing key elements.
3. **The Judge (Gemini 2.5 Meta-Optimizer)**: Acts as the Prompt Engineering Master. If the score is below target (e.g., < 85%), it reviews the error log, identifies spatial or layout misinterpretations, and embeds strategic new layout constraints into a brand-new generation prompt.

## Prerequisites & Installation

To run this project, make sure you install the required packages:

```bash
pip install google-genai pydantic pillow datasets