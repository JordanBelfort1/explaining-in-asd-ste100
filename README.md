# explaining-in-asd-ste100

An agent skill for Claude Code (and other agents that read `SKILL.md`). It makes the agent pick the best format for an explanation, instead of writing a wall of text by habit.

Based on Andrej Karpathy's post about the time we will spend understanding LLM output. Each rung of the ladder is better than the one before it:

**ASD-STE100 text → diagram (a sheet) → HTML page → explainer video**

ASD-STE100 is the language of every rung: the text, every label on the sheet, the page and the video narration.

- **Text** follows the full rules of ASD-STE100, the controlled language of aircraft maintenance documents. The skill maps the rules to **Polish** (simple words, verbs instead of nouns for actions, active voice, no adverbial participles, short sentences). If you write in English, it uses the original ASD-STE100 rules. "80% ASD-STE100" softens the rules on request.
- **Diagram = a sheet** in the style of a technical drawing, like Karpathy's ASD-STE100 overview: a frame with zones 1–8 / A–D, 3–6 lettered panels with one visual device each (tree, annotated specimen, status table, dictionary, limit bars, timeline), real examples, and a title block. One screen, white paper, blue = correct, red = wrong. See [sheet.md](sheet.md) and [sheet-template.html](sheet-template.html).
- **HTML page:** a sheet plus interaction inside the panels (step through, before/after, filters).
- **Explainer video:** 3Blue1Brown style with Manim, or Remotion. Narration from ElevenLabs (`ELEVENLABS_API_KEY`) or free local TTS (Piper, Kokoro). The agent asks before it starts. See [video.md](video.md).

## Install

```bash
git clone https://github.com/JordanBelfort1/explaining-in-asd-ste100 ~/.claude/skills/explaining-in-asd-ste100
```

The skill starts by itself when you ask the agent to explain something ("wyjaśnij", "nie rozumiem", "co to jest", "explain"), or when you ask for a format by name ("w HTML", "zrób diagram", "film w stylu 3b1b").

## License

MIT
