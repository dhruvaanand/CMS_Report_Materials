# Archi Issues Log

---

| # | Issue | Description | Fix (one line) | Priority |
|---|-------|-------------|----------------|----------|
| 1 | Domain knowledge gap | LLM misinterprets CMS-specific terms that share meaning with general English, e.g. draining, CouchDB | Extend skills system with corpus co-occurrence mining to auto-maintain CMS-specific term definitions | High |
| 2 | Brittle vector search | Static general-purpose embedding model produces weak representations for CMS operational queries, causing retrieval to fall below threshold | Fine-tune sentence transformer on auto-generated CMS query-document training pairs on every ingestion | High |
| 3 | Poor chunking | CharacterTextSplitter splits atomic units like runbook steps and glossary entries mid-sentence across chunk boundaries | Implement a Document Structure Aware Chunker with per-document-type heuristic splitting rules | High |
| 4 | Static alpha weighting | BM25 and vector score are blended at a fixed ratio regardless of whether the query is a lookup or a diagnostic question | Use query classifier to set alpha dynamically per query type | Medium |
| 5 | Single-shot retrieval | One retrieval attempt per query with no fallback if results are poor | Graph-augmented PostgreSQL maps entity relations so related chunks are fetched together via SQL joins | Medium |
| 6 | No reranking | Initial BM25 and vector combined score is used directly without a relevance verification pass | Add a cross-encoder reranker to rescore top-k chunks before passing to the LLM | Medium |
| 7 | No query rewriting | Raw operator queries including terse shorthand are sent directly to the retriever without reformulation | Single lightweight model call rewrites query into retrieval-optimised form before each retrieval | Medium |
| 8 | No conversation memory | Each query is treated independently with no awareness of prior turns in the same session | Maintain a structured entity buffer across turns and incorporate it into query rewriting | Medium |
| 9 | No confidence scoring | Model presents uncertain answers with the same tone as confident ones, no signal for the operator | Three-layer framework: retrieval score gate, logprob span scoring, lexical entity verification | High |
| 10 | No source transparency | Operator has no visibility into which document each statement was retrieved from | Prompt LLM to annotate claims with source chunk IDs, verified by NLI cross-encoder pass | Medium |
| 11 | No recency weighting | Old resolved tickets carry the same retrieval weight as recent alerts and shift handover notes | Add a gamma decay variable to the retrieval score formula, tuned per document type | Medium |
| 12 | No conflict detection on ingest | When a runbook is updated, old and new chunks coexist and the retriever may return contradictory procedures | Check new normative document uploads against existing content and overwrite with audit trail | Medium |
| 13 | Tool selection failure | Smaller local models called the wrong retrieval tool or printed raw JSON instead of executing the tool call | Add retry logic and better tool descriptions in config, surface structured error on persistent failure | Low |
| 14 | No evaluation harness | No automated way to measure whether changes to the pipeline actually improve performance | Implement RAGAs evaluation pipeline with a stratified test set segmented by query class | Medium |
| 15 | Gemini rendering bug | Gemini thought signatures surfaced as raw text in the model output due to content block handling incompatibility | Extract text field from content blocks and handle thought signatures separately in base_react.py | Low |
