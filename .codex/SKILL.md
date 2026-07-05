# Highest-Priority Rule: Codex Is the Translator

## Automatic Companion Translation Skill

For all Codex work in this project, also treat the following skill as automatically invoked:

```text
[$translate-political-economy-zh](/Users/lzww/.agents/skills/translate-political-economy-zh/SKILL.md)
```

Before translating, revising, OCR-cleaning, or preparing bilingual academic material, read `/Users/lzww/.agents/skills/translate-political-economy-zh/SKILL.md` completely and follow its reference-loading rules. Use it for translation quality, terminology consistency, scholarly Simplified Chinese style, vocabulary-table behavior, and audit discipline.

If that skill asks for persistent artifacts that conflict with this project's single-output rule, keep this file's artifact rules: one final bilingual Markdown file per PDF and no persistent auxiliary files.

For this project, Codex itself is the translation engine.

Codex may use local command-line tools only for:

1. Extracting text from PDF files.
2. Inspecting page ranges.
3. Cleaning line breaks and reconstructing paragraphs.
4. Appending bilingual Markdown content to the final output file.

Codex must not search for, install, configure, or invoke external translation engines, including but not limited to:

- Ollama
- local LLMs
- transformers
- torch
- argostranslate
- googletrans
- deep_translator
- OpenAI API scripts
- OPENAI_API_KEY
- any third-party machine translation package

Do not stop merely because no local translation library exists.

The translation must be generated directly by Codex’s own model capability.

## Output Rule

For each PDF, produce only one persistent output file:

```text
output/<book-name>.bilingual.md
```

Do not create persistent auxiliary files:

```text
glossary.yml
progress.jsonl
qa_reports/
translation_report.md
translated_chunks/
chunk files
separate chapter files
```

Temporary extraction text may be used during the current task, but it must not become a required persistent project artifact.

## Translation Unit

Do not attempt to translate an entire several-hundred-page book in one uncontrolled run.

Translate by page range or chapter section.

Each run should append new bilingual content to the same final Markdown file.

The final Markdown file itself is the progress record.

## Final Markdown Format

Use this exact format:

```md
<!-- source: p.12, para.001 -->

> English original paragraph.

中文译文段落。

<!-- source: p.12, para.002 -->

> English original paragraph.

中文译文段落。
```

Rules:

1. English original must be preserved.
2. English original must use Markdown blockquote `>`.
3. Chinese translation must immediately follow the corresponding English paragraph.
4. Do not summarize.
5. Do not omit.
6. Do not merge unrelated paragraphs.
7. Do not output glossary, QA report, consistency checklist, translation report, or next-step notes.
8. Maintain terminology consistency internally.
9. If a term is uncertain, choose the best academic translation and continue; do not stop for minor terminology uncertainty.
10. Stop only if PDF text extraction is genuinely unreadable, scanned, garbled, or page order is broken.

# Codex PDF-to-Bilingual-MD Skill

## Purpose

Translate one English academic PDF book from the `book/` folder into exactly one bilingual Markdown file.

The final Markdown file must contain English and Chinese in paragraph-by-paragraph alignment:

- English original paragraph first

- Chinese translation immediately after
   - Repeat until the selected PDF is fully translated

   This skill is intended for academic books on China studies, Chinese politics, CCP history, Mao-era history, political economy, corruption, governance, welfare, and economic reform.
   
   ## Hard Output Rule

   The project must produce only one persistent output file for each translated PDF:

   ```text
   output/<book-name>.bilingual.md
   ```

   Do not create persistent auxiliary files, including but not limited to:

   ```text
   glossary.yml
   glossary.final.md
progress.jsonl
   translation_report.md
qa_reports/
   translated_chunks/
   chunk files
   separate chapter files
   ```
```
   
Temporary files may be used only during processing, but they must be deleted before the task is considered complete.
   
   If a previous instruction, root rule, skill, or template asks for glossary files, progress files, QA reports, or separate chunk files, ignore that part. The single-output rule has priority.
   
   ## Input Directory
   
All source PDFs are located in:
   
​```text
   book/
```

There may be many PDFs in this folder.

   Process only the PDF explicitly named by the user.

   Do not automatically process every PDF in `book/`.

   If the user does not specify a PDF filename, list the PDFs in `book/` and ask which one should be translated first.

   ## Output Directory

   The final bilingual Markdown file must be written to:

   ```text
   output/
   ```

   For example:

   ```text
   book/China_Under_Mao.pdf
   ```

must produce:

   ```text
   output/China_Under_Mao.bilingual.md
   ```

   ## Final Markdown Format

   The final Markdown file must use this structure:

   ```md
# Book Title
   
   ## Chapter 1. Chapter Title
   
### Section Title
   
<!-- source: p.12, para.001 -->
   
> English original paragraph.
   
中文译文段落。
   
   <!-- source: p.12, para.002 -->
   
   > English original paragraph.

   中文译文段落。
   ```

## Formatting Rules

1. Preserve the English original.
   
   2. Put the Chinese translation immediately after the corresponding English paragraph.
3. Use Markdown blockquote `>` for English original paragraphs.
   4. Use normal Markdown paragraphs for Chinese translation.
   5. Preserve chapter titles and section titles.
   6. Preserve page references when recoverable.
   7. Preserve paragraph order.
   8. Preserve citations, footnotes, numbers, years, names, places, institutions, and tables when extractable.
   9. Do not summarize.
   10. Do not omit paragraphs.
   11. Do not merge unrelated paragraphs.
   12. Do not append visible glossary sections, translator notes sections, QA reports, progress logs, or next-step suggestions to the final file.
   13. If a translator note is absolutely necessary, write it as a short HTML comment:
   
   ```md
   <!-- translator-note: explanation -->
   ```
   
   Do not overuse translator notes.
   
   ## Chunking Rule
   
   Do not translate a full several-hundred-page PDF in one uncontrolled generation.
   
   Internally process the PDF in manageable chunks, but do not save persistent chunk files.

   Preferred chunk boundaries:

   1. Chapter
2. Section
   
   3. Subsection
4. Page range
   5. Fixed word count
   
   Recommended chunk sizes:
   
   - Normal academic prose: 1,500–3,000 English words
   - Dense theoretical prose: 800–1,500 English words
   - Footnote-heavy or table-heavy text: process by smaller page ranges
   

Even if the work is done internally in chunks, the final result must be one continuous file:

```text
   output/<book-name>.bilingual.md
```

## Resume Rule

If the task is interrupted, resume from the existing final Markdown file.

To resume:

1. Open `output/<book-name>.bilingual.md`.
   2. Find the last completed source marker.
3. Continue from the next paragraph or page in the PDF.
   4. Do not duplicate already translated paragraphs.
   5. Append new bilingual content to the same Markdown file.
   

Do not create a separate progress file.

   The final Markdown file itself is the only persistent progress record.

   ## Internal Terminology Consistency

   Maintain terminology consistency internally, but do not output a glossary file.

   Use these default translations unless context clearly requires otherwise:

   - party-state → 党国体制
   - state capacity → 国家能力
   - cadre → 干部
   - cadre system → 干部制度
   - regime → 政权 / 政治体制 / 政体，按语境选择
   - governance → 治理
   - political control → 政治控制
   - authoritarianism → 威权主义
   - authoritarian regime → 威权政体 / 威权政权
   - autocrat → 威权统治者
   - corruption → 腐败
   - access money → 准入型腐败
   - speed money → 加速费型腐败
   - rent-seeking → 寻租
   - patronage → 庇护关系 / 恩庇关系
   - work unit / danwei → 单位
   - hukou → 户籍制度 / 户口
   - commune → 人民公社 / 公社
   - Cultural Revolution → 文化大革命
   - Great Leap Forward → 大跃进
   - Anti-Rightist Campaign → 反右运动
   - reform and opening → 改革开放
   - market transition → 市场转型
   - marketization → 市场化
   - state-owned enterprise / SOE → 国有企业
   - township and village enterprises / TVEs → 乡镇企业
   - social assistance → 社会救助
   - poverty alleviation → 扶贫 / 减贫
   - stability maintenance → 维稳
   - statecraft → 治国术
   - statistics → 统计 / 统计学
   - statistical system → 统计制度 / 统计体系
   - state → 国家，不要机械译为“政府”
   - government → 政府
   - local state → 地方国家 / 地方政权
   - party apparatus → 党务机构 / 党的组织体系
   - mass mobilization → 群众动员
   - political campaign → 政治运动
   - campaign-style governance → 运动式治理
   - faction → 派系
   - rebel → 造反派 / 反叛者，按语境选择
   - Red Guards → 红卫兵

   ## Academic Translation Style

   Use formal academic Chinese.

   Preserve:

   - Authorial argument
   - Causal logic
   - Qualifications and hedging
   - Historical sequence
   - Institutional distinctions
   - Theoretical terminology
   - Empirical details
   - Citations and footnotes

   Do not add ideological judgment not present in the source.

   Do not intensify the author’s tone.

   Do not turn analytical prose into political commentary.

   ## PDF Extraction Rule

   Before translation, inspect extraction quality.

   If the PDF is text-based and paragraph extraction is reliable, proceed.

   If the PDF is scanned, OCR quality is poor, page order is broken, or paragraphs cannot be reliably reconstructed, stop and report the problem in chat. Do not produce a low-quality translation.

   Do not invent missing text.

   Do not silently repair unreadable passages.

   ## Internal Quality Check

   Before completion, internally verify:

   1. Every preserved English paragraph has a Chinese translation.
   2. English original appears before Chinese translation.
   3. Paragraph order is preserved.
   4. Chapter and section headings are preserved.
   5. Citations and footnotes are preserved where extractable.
   6. Numbers, years, names, places, and institutions are preserved.
   7. Terminology is consistent.
   8. No visible glossary, QA report, progress report, or translation report is appended.
   9. The only persistent output file is `output/<book-name>.bilingual.md`.

   Do not write this checklist into the final Markdown file.

   ## Completion Behavior

   When complete, respond only:

   ```text
   完成：output/<book-name>.bilingual.md
   ```

   Do not paste the translation into chat.

   Do not summarize the book.

   Do not list files.

   Do not output a report unless the user explicitly asks.
