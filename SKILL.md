---
name: explaining-in-asd-ste100
description: Use when the user asks to explain, understand or make sense of something (a concept, a process, a diff, a PR, an agent's output, a review result, a question you just asked them), says they still do not understand, or asks for an explanation as text, ASD-STE100, a diagram, an HTML page or an explainer video. Polish triggers - "wyjaśnij", "wytłumacz", "nie rozumiem", "co to jest", "czym jest", "o co chodzi", "pomóż mi zrozumieć", "zrób diagram", "zrób stronę", "film wyjaśniający", "w stylu 3b1b".
---

# Explaining in ASD-STE100

## Overview

Source: Andrej Karpathy's post on understanding LLM output. More of the user's work moves up the abstraction ladder, to supervision and understanding. Models can help: intelligence and code are now abundant, so a large, custom, one-off artifact (a web app, an explainer video) that never made sense before makes sense now. **Push the limits here.**

Each rung is better than the one before it ("but even better"):

**ASD-STE100 text → diagram (a sheet) → HTML page → explainer video**

All rungs use **ASD-STE100**. It is the language of every explanation, on every rung.

## The reply

Every explanation reply has these parts, in this order, and nothing else:

1. **The answer in one ASD-STE100 sentence.** It answers the question. It is not "Dobre pytanie", "Przepraszam" or "Sprawdzam".
2. **The rung output:** the ASD-STE100 text, or the sheet, the page or the video (link or path).
3. **The offer of the next rung up, in one line**, up to the video. Example: "Mogę z tego zrobić film wyjaśniający w stylu 3b1b, z narracją."

**Text budget in the terminal:** about 250 words on the text rung, about 120 words next to a sheet or a page. When the answer needs more words, it needs a higher rung. Make the higher rung now.

## Choose the rung

Use the first row that matches. When two rows match, take the higher rung. If you are not sure, take the higher rung.

| Observable condition | Rung |
|---|---|
| The user asks for a format by name ("w HTML", "diagram", "film") | That format |
| The user still does not understand after an earlier explanation in this session | One rung higher than the last explanation. After an HTML page: ask about the video (see Rung 4) |
| The user asks for a film, or wants to watch something | Video, after confirming |
| The reader must step through it, compare states, toggle before/after or filter many items | HTML page |
| It has parts, a sequence, a decision, a flow, a comparison, several findings, or it needs more than the text budget | Diagram: a sheet |
| The answer is one fact that fits in about 3 ASD-STE100 sentences | ASD-STE100 text |

**This skill stays active for the whole session.** Every later explanation follows it: an answer inside a review, a plan, a status report, or after an AskUserQuestion. When the user answers your question with "nie rozumiem" or "po co", explain first (with the rung from the table), then ask again. Never refer to a picture, sheet or page that the user has not seen.

## The language: ASD-STE100 in Polish

**Write every explanation in Polish, by the rules of ASD-STE100.** ASD-STE100 (Simplified Technical English) is the controlled language of aircraft maintenance documents. The specification is for English, so use its rules as mapped to Polish below: all of them, not only sentence length. This covers every rung: the text, every label on the sheet, the page copy and the video narration. If the user writes in English, use the original ASD-STE100 rules in English.

The default is full ASD-STE100: follow every rule. If the user asks to soften it ("80% ASD-STE100", "80% drogi do ASD-STE100", "złagodź"), you may keep a necessary technical word or a sentence that is a little longer.

**Words**
- Use simple, common words: "użyj", not "wykorzystaj" or "zastosuj"; "sprawdź", not "zweryfikuj"; "zacznij", not "zainicjuj"; "upewnij się", not "zapewnij"; "zrób", not "dokonaj" or "przeprowadź"; "około", not "w przybliżeniu"; "żeby", not "w celu".
- Use a verb for an action, not a noun made from a verb: "sprawdź plik", not "dokonaj sprawdzenia pliku"; "serwer podpisuje", not "następuje złożenie podpisu"; "decyduje", not "podejmuje decyzję".
- One word has one meaning, and one thing has one word. If you write "gałąź", write "gałąź" every time, not "branch" in one place and "odgałęzienie" in another.
- Technical names (TLS, ClientHello, `main`, PR, Vercel) are permitted. Write them exactly as the source does and do not translate them.

**Verbs**
- Use the present, past and future tenses in the indicative mood. Use the imperative for instructions.
- Use the active voice and name who does it: "serwer zapisuje plik", not "plik jest zapisywany" or "plik zapisano".
- Do not use adverbial participles ("-ąc", "-wszy", "-łszy"). They are the Polish equivalent of the "-ing" form that ASD-STE100 forbids. Write two sentences, or join them with "i", "potem" or "gdy".
- Use the passive adjectival participle only as an adjective ("podpisana wiadomość").
- Do not use the conditional for a fact: "Git tworzy commit", not "Git utworzyłby commit".

**Sentences and paragraphs**
- The first sentence answers the question.
- One idea per sentence. An instruction has at most 20 words. A description has at most 25 words.
- One topic per paragraph, at most 6 sentences, topic sentence first.
- A chain of genitive nouns has at most 3 nouns: "klucz serwera" is correct; "konfiguracja środowiska budowania produkcji" is too long. Keep connectors, and do not write in telegraph style.
- Use a numbered list for steps and a bullet list for 3 or more parallel items.

## Rung 1: ASD-STE100 text

The explanation in ASD-STE100, within the text budget.

## Rung 2: Diagram = a sheet

A sheet is one page in the style of a technical drawing, like Karpathy's ASD-STE100 overview: a frame with zones, 3–6 lettered panels, one visual device per panel, real specimens, and a title block. The reader sees the whole answer at one look. **REQUIRED:** follow [sheet.md](sheet.md) and start from [sheet-template.html](sheet-template.html).

An ASCII diagram in the terminal is only for a flow of at most 5 boxes inside a text answer, or when the user asks for the answer in the terminal.

## Rung 3: HTML page

The page **starts with a sheet** ([sheet.md](sheet.md)) and adds interaction inside the panels: step through the timeline, toggle before/after on a specimen, filter a status table, "what does each party know now". The interaction must help understanding, not decorate. Publish it like the sheet (Artifact, or `.html` plus PNG).

## Rung 4: Explainer video

It takes a long time and can cost money (voice API). **Confirm first** in a single question: length, voice (paid or free) and output folder. The narration is in Polish ASD-STE100 unless the user names another language. Then follow [video.md](video.md).

## Supervision: understanding agent output

When the subject is a diff, a PR, an audit or an agent report:
- The verdict is the first sentence of the reply and the title of the sheet.
- A change to flow or structure → a sheet with a before/after panel.
- Several findings → a sheet: one panel per group, a status table per panel. Many findings that the reader must filter → an HTML page.

## Common mistakes

| Mistake | Correct |
|---|---|
| 400+ words of text in the terminal | A sheet, and at most 120 words next to it |
| Text again after "nadal nie rozumiem" | One rung higher than the last explanation |
| A long, dark landing page with prose sections | A sheet: panels, specimens, title block, one screen |
| "Dobre pytanie." as the first sentence | The answer as the first sentence |
| A new question that points at a drawing the user did not see | The explanation first, then the question |
