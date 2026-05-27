# 🪩 Annotation UIs

A shared collection of annotation interfaces built by the Guide AI team at Stanford. Each UI is a self-contained HTML file designed to collect structured feedback from clinicians and domain experts on AI-generated outputs.

**The value of this repository is less about the code and more about the UI designs we converged on across projects.** These interfaces represent iterative design decisions — layout patterns, labeling taxonomies, interaction flows — that were refined through real annotator feedback. By sharing them here, we avoid reinventing the wheel and maintain consistency in how we collect human evaluations.

## 🛸 Contributing

If you work on the Guide AI team and your project involved building a custom annotation UI with feedback from users, **we encourage you to upload it here**. Building these single-file annotation UIs is a great use case for agentic coding — the design choices and annotator-facing decisions are what matter, and future projects benefit from seeing what worked.

To add a UI:
1. Place your `.html` file (or folder, if it has assets) in the `uis/` directory.
2. Add a brief entry to the table below describing what it does and what data it targets.

## 🧊 Available UIs

All files live in the [`uis/`](uis/) directory.

| File | Annotation Target | Description | HTML Preview |
|------|-------------------|-------------|--------------|
| `chatehr_annotation_ui.html` | ChatEHR UI responses | Evaluates AI-generated clinical summaries. Annotators identify hallucinations, inaccuracies, and omissions, rate potential harm severity (Levels 1–4), and provide free-text justifications. Outputs a JSON payload tagged with `#chatehreval` for clipboard export. | [preview](https://htmlpreview.github.io/?https://github.com/som-guideai/annotation-UIs/blob/main/uis/chatehr_annotation_ui.html) |
| `ellis_caleo_ui.html` | Tumor board summaries | Annotates AI-generated tumor board summaries. Same issue taxonomy (hallucinations, inaccuracies, omissions) with harm-level ratings. Writes annotations incrementally to a local CSV file via the File System Access API (Chrome or Edge only). | [preview](https://htmlpreview.github.io/?https://github.com/som-guideai/annotation-UIs/blob/main/uis/ellis_caleo_ui.html) |
| `verifact_comparison.html` | VeriFactB predictions | Side-by-side comparison of human clinician annotations against VeriFactB automated predictions. Annotators draw edges to map matching findings between the two sets, enabling evaluation of automated fact-verification accuracy. Saves to CSV. | [preview](https://htmlpreview.github.io/?https://github.com/som-guideai/annotation-UIs/blob/main/uis/verifact_comparison.html) |

## 🔬 How They Work

All UIs run entirely in the browser — just open the `.html` file locally. No server, no build step, no external dependencies.

## 🔐 Integration and Security

Because these UIs are used to annotate PHI data, everything runs locally on the annotator's machine. **Always download the HTML files and open them locally** — do not use the previews above for actual annotation work, as those are rendered by a third-party service and are not secure for handling PHI.

Final annotations are shared via standard secure channels:

- **Secure email** — for CSV-based UIs, the annotator emails the completed file.
- **Clipboard with tagged JSON** — for the ChatEHR UI, the annotator copies a JSON object prefixed with a regex-recognizable tag (`#chatehreval`) and pastes it into the ChatEHR free-text feedback field.

This keeps things simple and secure, but the lack of integration can create friction — there is no centralized aggregation or real-time visibility into annotation progress.

## 🧭 Future Direction

If this is worth exploring, we could partner with TDS Data Science to build the capability to securely deploy annotation UIs with tighter integration — behind a SID login, with annotations stored in secure places (e.g., SQL tables in Databricks). That infrastructure would then be reusable across projects on both the .edu and .org sides. A concrete starting point could be the ChatEHR annotation workflow for automations such as radiology, where annotations are already being actively collected.
