# Project Instructions

## Default Translation Skill

Every Codex thread opened in this workspace (`/Users/lzww/history`) must treat the following skill as automatically invoked, even when the user does not mention it:

`[$translate-political-economy-zh](/Users/lzww/.agents/skills/translate-political-economy-zh/SKILL.md)`

Before taking task actions in this project, read `/Users/lzww/.agents/skills/translate-political-economy-zh/SKILL.md` completely and follow its reference-loading rules when the task involves translation, OCR, article images, PDFs, book chapters, excerpts, terminology, bilingual drafts, vocabulary-learning output, or revision of Chinese academic prose.

Default to Simplified Chinese for English-to-Chinese translation. Preserve the author's argument, evidence, sequence, citations, proper nouns, institutional terms, quantitative claims, and neutral analytical register. For article-like English text or article images, include a concise core/difficult vocabulary table unless the user asks for translation only.

## Relationship To `.codex/SKILL.md`

The project-local `.codex/SKILL.md` remains binding for PDF-to-bilingual-Markdown work: Codex itself is the translation engine, external translation engines are forbidden, and each translated PDF should produce only one persistent output file at `output/<book-name>.bilingual.md`.

If `.codex/SKILL.md` conflicts with `translate-political-economy-zh` about persistent artifacts such as termbases, progress logs, QA reports, chunk files, or chapter packages, follow `.codex/SKILL.md` for artifact shape and file layout while still using `translate-political-economy-zh` for translation quality, terminology discipline, scholarly style, vocabulary behavior, and audit checks.

## Scope

This rule is project-local. It applies to Codex work rooted in `/Users/lzww/history` and does not change global Codex behavior outside this workspace.
