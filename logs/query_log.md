# Archi Query Log

Model: Gemini 2.5 Flash via API
Test documents: 9 CMS operational documents, 93 chunks in PostgreSQL with pgvector
Total queries: 21

---

| # | Question | Area Tested | Summary of Response | Rating |
|---|----------|-------------|---------------------|--------|
| 1 | What happened in CMSPROD-4821? | Ticket recall | Correct answer, but required 5 tool call attempts before retrieval was invoked | Pass |
| 2 | What was the root cause of CMSTRANSF-1094? | Diagnostic / ticket recall | Correctly identified GridFTP 530 auth error, cross-referenced runbook | Pass |
| 3 | Which sites were affected in CMSPROD-5103? | Factual recall | Correctly returned T2_IT_Bari (78%), T2_IT_Rome (71%), CVMFS | Pass |
| 4 | What is CouchDB? | Domain knowledge / glossary lookup | Returned a generic NoSQL database description, ignored the CMS-specific glossary entry entirely | Fail |
| 5 | What is WMAgent? | Domain knowledge / glossary lookup | Returned the correct CMS-specific definition from the glossary | Pass |
| 6 | What is Acquired state? | Domain knowledge / glossary lookup | Correct, including the 2-3 hour threshold, sourced from both glossary and runbook | Pass |
| 7 | How do I investigate a stuck workflow? | Procedural | Accurate step-by-step response but noticeably verbose | Pass |
| 8 | What are the steps for handling a transfer failure? | Procedural | Comprehensive, correct error categorisation across multiple steps | Pass |
| 9 | When should I use Force Complete? | Procedural | Correct but incomplete, missed some edge cases | Partial |
| 10 | How does CouchDB disk exhaustion relate to draining? | Diagnostic / multi-document | Correctly synthesised information across multiple documents | Pass |
| 11 | How do you distinguish site-level from central failures? | Diagnostic | Referenced CMSPROD-5103 and CMSPROD-5298 correctly | Pass |
| 12 | What is the current status of T2_US_MIT? | Live data / scope boundary | Correctly declined, noted it has no access to live monitoring data | Pass |
| 13 | Who is the current shift operator? | Live data | Server error due to API rate limit on free tier | Error |
| 14 | Why would WMAgent stop submitting jobs? | Diagnostic | Synthesised correctly across 4 documents | Pass |
| 15 | Jobs are failing at an Italian site, what should I check? | Diagnostic | Correctly identified CVMFS Stratum-1 as primary suspect | Pass |
| 16 | Which tickets were resolved within 24 hours? | Factual recall | Correctly returned CMSPROD-4821 (3h15m) and CMSTRANSF-1094 (5h25m) | Pass |
| 17 | Which alerts would require immediate escalation? | Factual / procedural | Correctly identified CRITICAL threshold and T0TapeWriteStall | Pass |
| 18 | What is the difference between Acquired and Running state? | Domain knowledge | Clear distinction, correct sources cited | Pass |
| 19 | What is the CMS detector made of? | Out of scope | Correctly declined, identified query as outside knowledge base scope | Pass |
| 20 | Was there a follow-up ticket after CMSPROD-4821? | Ticket recall | Correctly returned CMSPROD-4822. Gemini rendering bug visible in output. | Pass |
| 21 | What was the disk usage percentage when CouchDB issue was detected? | Factual recall | Correctly admitted the specific figure was not present in the documents | Pass |

---

Results: 19 pass, 1 fail, 1 partial, 1 server error (API rate limit)
