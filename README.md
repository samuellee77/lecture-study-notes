# Lecture Study Notes

A Codex skill that turns lecture slides, transcripts, and course readings into comprehensive study notes with diagrams and interactive HTML companions.

The goal is to help students understand the material without repeatedly returning to the slides. Notes follow the course's terminology and explain the connections between definitions, formulas, algorithms, examples, and results.

## What it produces

By default, each lecture gets:

- A Markdown note with connected explanations, defined notation, worked examples, and review questions with answers.
- A self-contained HTML companion with the same teaching content and focused interactive demonstrations when useful.
- Figures with captions and reading guides where visual explanations improve understanding.

Multi-lecture collections also get a Markdown index with links to both formats. Explicit requests for shorter summaries, formula sheets, a particular language, or a single output format override the defaults.

Examples of useful interactions include changing optimizer parameters, stepping through an algorithm, comparing worker delays, exploring client drift, and selecting items to see coverage and marginal gains. The choice depends on the lecture; the skill does not impose a fixed set of demonstrations.

## Install

### Through Codex

Paste this prompt into Codex:

```text
Use $skill-installer to install the lecture-study-notes skill from
https://github.com/samuellee77/lecture-study-notes,
at path skills/lecture-study-notes.
```

The skill installer is included in standard Codex installations. The installed skill becomes available on the next turn; reopen your Codex session if it does not appear.

### Manual installation on macOS or Linux

Clone this repository, enter its folder, and copy the skill:

```bash
git clone https://github.com/samuellee77/lecture-study-notes.git
cd lecture-study-notes
skill_target="${CODEX_HOME:-$HOME/.codex}/skills/lecture-study-notes"
if [ -e "$skill_target" ]; then
  printf 'A skill already exists at %s. Back it up or remove it before installing.\n' "$skill_target"
else
  mkdir -p "$(dirname "$skill_target")"
  cp -R skills/lecture-study-notes "$skill_target"
fi
```

On Windows, copy `skills/lecture-study-notes` into the `skills` folder under your Codex home directory (normally `%USERPROFILE%\.codex`).

The installed folder must contain `SKILL.md` directly, with `agents/openai.yaml` beneath it. Do not copy the entire repository into the installed skill folder.

## Use

Give Codex access to your lecture materials and specify the lectures and destination:

```text
$lecture-study-notes
Create comprehensive review notes for lectures/lec2.pdf and lectures/lec3.pdf.
Save each lecture separately in notes/.
```

To upgrade an existing collection:

```text
$lecture-study-notes
Rewrite the notes in notes/ using the matching PDFs in lectures/.
Make them self-contained, explain the formulas, and add interactive
HTML companions where demonstrations help understanding.
```

For a smaller deliverable:

```text
$lecture-study-notes
Make a concise Markdown-only formula sheet for lectures/lec4.pdf.
Define each symbol and state the assumptions for each result.
```

You can also request a language, an audience level, or particular concepts to emphasize.

## Output layout

A typical collection looks like this:

```text
notes/
├── README.md
├── lecture-2-review.md
├── lecture-2-review.html
├── lecture-3-review.md
├── lecture-3-review.html
└── figures/
```

Open the HTML files in a browser. Their content, equations, figures, and demonstrations should work without a server or internet connection. Links to source documents or other notes still depend on those files being present. Keep the collection together when sharing it.

## Requirements and verification

This repository contains instructions and Codex interface metadata, rather than a standalone converter or a bundled rendering engine. There are no mandatory package-install commands for the skill itself.

Codex needs read access to the source material and write access to the output folder. Depending on the input and requested output, it may use PDF extraction and page-rendering tools, plotting libraries, local math-rendering assets, and browser tools. Available dependencies differ across environments; the skill directs Codex to inspect available tools and report any verification it could not perform.

The workflow checks source coverage, formula assumptions and normalization, numerical examples, figure readability, and links. HTML verification includes controls, resets, keyboard use, and a narrow viewport when browser tools are available. Synthetic examples must be labeled separately from course experiment results.

## Sharing and contributions

Share only source materials and generated notes you have permission to distribute. Installing this skill does not grant redistribution rights to lecture slides, recordings, readings, or third-party assets.

For improvements, open an issue with a small reproducible example and the expected behavior. Include source excerpts only when you have permission to share them. Keep changes general enough to work across courses and preserve explicit user choices about format and scope.

## Repository contents

- [`skills/lecture-study-notes/SKILL.md`](skills/lecture-study-notes/SKILL.md): the reusable workflow.
- [`skills/lecture-study-notes/agents/openai.yaml`](skills/lecture-study-notes/agents/openai.yaml): Codex display metadata and default prompt.

No course PDFs, private notes, generated course figures, or machine-specific rendering dependencies are included.
