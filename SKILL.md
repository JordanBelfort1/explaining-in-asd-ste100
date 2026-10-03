---
name: choosing-explanation-format
description: Use when the user asks to explain, understand or make sense of something (a concept, a process, a diff, a PR, an agent's output, a review result), says they still do not understand, or asks for an explanation as text, ASD-STE100 / STE, a diagram, an HTML page or an explainer video. Polish triggers - "wyjaśnij", "wytłumacz", "nie rozumiem", "pomóż mi zrozumieć", "zrób diagram", "zrób stronę", "film wyjaśniający", "w stylu 3b1b".
---

# Choosing the explanation format

## Overview

Source: Andrej Karpathy's post on understanding LLM output. More of the user's work moves up the abstraction ladder, to supervision and understanding. Models can help: intelligence and code are now abundant, so a large, custom, one-off artifact (a web app, an explainer video) that never made sense before makes sense now. **Push the limits here.**

Each rung is better than the one before it ("but even better"):

**STE text → diagram → HTML page → explainer video**

## The recipe

Every explanation has these parts, in this order:

1. **Choose the rung.** Use the first row in the table that matches. When two rows match, take the higher rung.
2. **Make it.** Follow the section for that rung.
3. **Offer the next rung up in one line**, up to the video. Example: "Mogę z tego zrobić film wyjaśniający w stylu 3b1b, z narracją."

| Observable condition | Rung |
|---|---|
| The user asks for a format by name ("w HTML", "diagram", "film") | That format |
| The user still does not understand after an earlier explanation | One rung higher than last time |
| The user asks for a film, or wants to watch something | Video, after confirming (see below) |
| The explanation does not fit on one terminal screen; it needs interaction (compare, step through, toggle); it is agent output with several findings; or other people will read it | HTML page, made now (not only offered) |
| It has a sequence, a decision, a flow, a structure or a before/after, and a diagram plus at most about 120 words fits on one screen | Diagram, with STE text around it |
| The answer is one fact that fits in about 3 sentences | STE text |

If you are not sure between two rungs, take the higher one.

**Length budget for text in the terminal: about 250 words.** If the answer needs more, move up a rung. Do not write more text.

## The language: ASD-STE100 in Polish

**Write every explanation in Polish, by the rules of ASD-STE100.** ASD-STE100 (Simplified Technical English) is the controlled language of aircraft maintenance documents. The specification is for English, so use its rules as mapped to Polish below: all of them, not only sentence length. This covers every rung: the text, the diagram labels, the page copy and the video narration. If the user writes in English, use the original STE rules in English.

The default is full STE: follow every rule. If the user asks to soften it ("80% STE", "80% drogi do STE", "złagodź"), you may keep a necessary technical word or a sentence that is a little longer.

**Words**
- Use simple, common words: "użyj", not "wykorzystaj" or "zastosuj"; "sprawdź", not "zweryfikuj"; "zacznij", not "zainicjuj"; "upewnij się", not "zapewnij"; "zrób", not "dokonaj" or "przeprowadź"; "około", not "w przybliżeniu"; "żeby", not "w celu".
- Use a verb for an action, not a noun made from a verb: "sprawdź plik", not "dokonaj sprawdzenia pliku"; "serwer podpisuje", not "następuje złożenie podpisu".
- One word has one meaning, and one thing has one word. If you write "gałąź", write "gałąź" every time, not "branch" in one place and "odgałęzienie" in another.
- Technical names (TLS, ClientHello, `main`, PR, Vercel) are permitted. Write them exactly as the source does and do not translate them.

**Verbs**
- Use the present, past and future tenses in the indicative mood. Use the imperative for instructions.
- Use the active voice and name who does it: "serwer zapisuje plik", not "plik jest zapisywany" or "plik zapisano".
- Do not use adverbial participles ("-ąc", "-wszy", "-łszy"). They are the Polish equivalent of the "-ing" form that STE forbids. Write two sentences, or join them with "i", "potem" or "gdy".
- Use the passive adjectival participle only as an adjective ("podpisana wiadomość").
- Do not use the conditional for a fact: "Git tworzy commit", not "Git utworzyłby commit".

**Sentences and paragraphs**
- The first sentence answers the question.
- One idea per sentence. An instruction has at most 20 words. A description has at most 25 words.
- One topic per paragraph, at most 6 sentences, topic sentence first.
- A chain of genitive nouns has at most 3 nouns: "klucz serwera" is correct; "konfiguracja środowiska budowania produkcji" is too long. Keep connectors, and do not write in telegraph style.
- Use a numbered list for steps and a bullet list for 3 or more parallel items.

## Rung 1: STE text

The explanation in STE (see above), within the length budget.

## Rung 2: Diagram

- **Terminal:** ASCII or box-drawing characters in a code block, at most 78 characters wide. Mermaid does not render in the terminal.
- **Richer:** SVG in an Artifact. **REQUIRED SUB-SKILL:** artifact-diagramming (if you have it). With no Artifact tool, put the SVG in a self-contained `.html` file.
- The diagram carries the explanation. The text explains only what the diagram cannot show, in at most about 120 words.

## Rung 3: HTML page

- Publish it with the Artifact tool, after loading artifact-design (artifact-diagramming too if the page holds diagrams). It is private by default. If you have no Artifact tool, write one self-contained `.html` file to a temporary folder and open it in the browser.
- Make it beautiful and interactive: animations, step through a sequence, toggle before/after, "what does each party know now", filters on a long list. The interaction must help understanding, not decorate.
- Reply in the terminal with the link and a summary of 2–3 sentences.

## Rung 4: Explainer video

It takes a long time and can cost money (voice API). **Confirm first** in a single question: length, voice (paid or free) and output folder. The narration is in Polish STE unless the user names another language. Then follow [video.md](video.md).

## Supervision: understanding agent output

When the subject is a diff, a PR, an audit or an agent report:
- A change to flow or structure → a before/after diagram.
- Many findings or files → an HTML page that groups them, with the verdict at the top.
- Text → STE, verdict first, then evidence.
