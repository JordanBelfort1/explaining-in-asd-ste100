# Explanation sheet

The diagram rung is one **sheet**: a page in the style of a technical drawing. Karpathy's ASD-STE100 overview is the model.

**The key is the explanation in ASD-STE100.** The sheet is the form; every word on it follows the ASD-STE100 rules in SKILL.md. When the form and a clear explanation pull apart, the explanation wins.

Start from [sheet-template.html](sheet-template.html). Keep its frame, panel header, devices and title block. Replace the content.

## Choose the layout first

The frame, the title block and ASD-STE100 are the same on every sheet. The layout inside the frame follows the question. Find the question type in the user's words, then use its layout. [sheet-layouts.html](sheet-layouts.html) shows each layout with a wireframe and a working example of its device.

| The user asks | Layout | Focal panel (the 12-column field) | Other panels |
|---|---|---|---|
| "Czym jest X?", "Z czego to się składa?", "Jak działa projekt X?" as an overview | **Przegląd** | None: 3–6 equal panels (`span-3` to `span-5`) | One device each, all different |
| "Jak to działa?" about one mechanism, protocol, flow or architecture | **Mechanizm** | One large SVG diagram, `span-8` or `span-9`, `tall` | 1–2 small panels on the right: a specimen, limits or a status table |
| "Co się dzieje krok po kroku?", "Jak to się zmienia?", a lifecycle | **Klatki** | Frames (`frames`, `--n: 3` to `6`) across `span-12`. Each frame shows the state after one step | 1–2 panels below: what can go wrong, values |
| "Czym A różni się od B?", before and after, options | **Porównanie** | Comparison grid (`cmp`) across `span-12` or `span-9`. Same rows for each side; mark the rows that differ | A verdict panel: when to use A, when to use B |
| "Dlaczego?", "Skąd ten błąd?", a root cause | **Łańcuch** | Cause chain (`chain`) in `span-7` or `span-8`, from the root cause to the effect the user sees | The fix, and how to check it |

- The panel count follows the content, not the template: a sheet can have 2 panels or 6.
- In the Mechanizm, Klatki, Porównanie and Łańcuch layouts the focal panel takes at least half of the field. It is panel A.
- When a question has two types ("jak działa i dlaczego się psuje"), use the layout of the main question and put the other one in a small panel.
- Write the layout name in the title block field "Układ".

## The sheet has these parts, in this order

1. **Frame.** Zone strips with columns 1–8 and rows A–D around the field.
2. **Panels**, as many as the layout needs, lettered A–F in reading order: left to right, then top to bottom. The letters follow the position on the sheet, not the order you wrote the panels. Each panel answers one question about the subject. Each panel header has the letter in a black square, a title, and a small mono caption on the right (the source section or the kind of content, e.g. "przykłady z adnotacjami").
3. **One device per panel.** Choose it from the table below. Use a different device in each panel when the content permits.
4. **Real specimens in every panel:** real names, real values, real counts ("13 słów, limit 20", "31 536 000 s = 365 dni"), a wrong example next to the correct one.
5. **A note line** under a panel when it needs one: at most 2 sentences.
6. **The title block**, bottom right: Tytuł, Układ, Specyfikacja (or Temat), Właściciel, Dotyczy, Data, Arkusz "1 z 1", Źródło. Fill every field with real data: a URL, a file path, a PR number. Write "—" when a field has no data.

## Devices

| The content is | Device (class in the template) |
|---|---|
| Parts, layers, "what contains what" | Tree (`tree-root`, `tree-kids`) |
| One real example: a sentence, a header, a command, a line of code | Annotated specimen (`specimen`, `ann`, `ann bad`, `measure`) |
| Allowed / not allowed, works / breaks, before / after | Status table (`ok`, `no`) |
| Terms and their meanings | Dictionary table: term, meaning, correct example, wrong example |
| Values against a scale or a limit | Limit bars (`bar`, `track`, `fill`, `ticks`) |
| A sequence of events, steps or a history | Timeline (`timeline`) |
| A flow with branches, a protocol between parties | Inline SVG inside a panel: boxes, arrows and labels, in the same ink and colors |
| The state after each step | Frames (`frames`, `n`, `pic`, `cap`, `state`) |
| The same questions for A and B | Comparison grid (`cmp`, `h`, `k`, `diff`, `risk`) |
| A cause, the steps between, the effect | Cause chain (`chain`, `link root`, `by`, `link effect`) |

## Look

- **Every word on the sheet is in ASD-STE100** (Polish rules in SKILL.md): titles, labels, table cells, notes and the title block.
- White paper, dark ink, and two accents with a fixed meaning: **blue** = correct, approved, annotation; **red** = wrong, not approved, risk. Do not use a third accent color.
- IBM Plex Sans for content. IBM Plex Mono for specimens, metadata, captions and scales.
- Rules and frames are lines. Do not use shadows, gradients, rounded cards, icons or emoji. The only symbols are ✓ and ✗. ✓ means "correct" or "works", and ✗ means "wrong" or "breaks". Do not use them for priority or severity: write "Blokuje" or "Drobne" as plain text.
- Text is only labels, table cells and note lines. Do not write paragraphs on a sheet.
- Size follows the explanation. A short answer fits one screen of about 1600 × 860 px. When the explanation needs more, add rows of panels below; the frame and the zone strips grow with the field. Do not cut, shrink or compress an explanation to make it fit one screen. Each row still has panels with a device and specimens, not paragraphs.

## Check before you hand it over

1. Render the sheet to PNG in the light theme. Example on Windows:
   `msedge --headless=new --disable-gpu --hide-scrollbars --blink-settings=preferredColorScheme=1 --virtual-time-budget=5000 --window-size=1600,860 --screenshot=<out.png> file:///<sheet.html>` (`chrome` takes the same flags). For a taller sheet, raise the height in `--window-size` until the bottom of the frame shows. Headless Edge often renders the PNG before IBM Plex loads; a fallback mono font with wide spaces in the PNG is a render problem, not a sheet problem.
2. Look at the PNG. Check that the layout matches the question type. Find text that is cut off, labels that overlap, an empty panel and a panel with no specimen. Repair them and render again.
3. Read every label against the ASD-STE100 rules. Repair each sentence that breaks a rule.

## Deliver

- With the Artifact tool: publish the sheet (load artifact-design first). Reply with the link.
- With no Artifact tool: save the `.html` and the PNG to a temporary folder, and give both paths.
- In the reply, the first sentence answers the question in ASD-STE100. Then add one more sentence at most, and the offer of the next rung.
