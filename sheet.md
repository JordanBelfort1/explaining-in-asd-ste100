# Explanation sheet

The diagram rung is one **sheet**: a page in the style of a technical drawing. Karpathy's ASD-STE100 overview is the model. The reader gets the whole answer at one look, without scrolling.

Start from [sheet-template.html](sheet-template.html). Keep its frame, panel header, devices and title block. Replace the content.

## The sheet has these parts, in this order

1. **Frame.** Zone strips with columns 1–8 and rows A–D around the field.
2. **3–6 panels**, lettered A–F in reading order: left to right, then top to bottom. The letters follow the position on the sheet, not the order you wrote the panels. Each panel answers one question about the subject. Each panel header has the letter in a black square, a title, and a small mono caption on the right (the source section or the kind of content, e.g. "przykłady z adnotacjami").
3. **One device per panel.** Choose it from the table below. Use a different device in each panel when the content permits.
4. **Real specimens in every panel:** real names, real values, real counts ("13 słów, limit 20", "31 536 000 s = 365 dni"), a wrong example next to the correct one.
5. **A note line** under a panel when it needs one: at most 2 sentences.
6. **The title block**, bottom right: Tytuł, Specyfikacja (or Temat), Właściciel, Dotyczy, Data, Arkusz "1 z 1", Wersja, Źródło. Fill every field with real data: a URL, a file path, a PR number. Write "—" when a field has no data.

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

## Look

- White paper, dark ink, and two accents with a fixed meaning: **blue** = correct, approved, annotation; **red** = wrong, not approved, risk. Do not use a third accent color.
- IBM Plex Sans for content. IBM Plex Mono for specimens, metadata, captions and scales.
- Rules and frames are lines. Do not use shadows, gradients, rounded cards, icons or emoji. The only symbols are ✓ and ✗. ✓ means "correct" or "works", and ✗ means "wrong" or "breaks". Do not use them for priority or severity: write "Blokuje" or "Drobne" as plain text.
- Text is only labels, table cells and note lines. Do not write paragraphs on a sheet.
- **Every word on the sheet is in ASD-STE100** (Polish rules in SKILL.md): titles, labels, table cells, notes and the title block.
- The sheet fits one screen of about 1600 × 860 px. If the subject needs more, make a second sheet ("Arkusz 2 z 2"). Do not make one long page.

## Check before you hand it over

1. Render the sheet to PNG in the light theme. Example on Windows:
   `msedge --headless=new --disable-gpu --hide-scrollbars --blink-settings=preferredColorScheme=1 --virtual-time-budget=5000 --window-size=1600,860 --screenshot=<out.png> file:///<sheet.html>` (`chrome` takes the same flags).
2. Look at the PNG. Find text that is cut off, labels that overlap, an empty panel and a panel with no specimen. Repair them and render again.
3. Read every label against the ASD-STE100 rules. Repair each sentence that breaks a rule.

## Deliver

- With the Artifact tool: publish the sheet (load artifact-design first). Reply with the link.
- With no Artifact tool: save the `.html` and the PNG to a temporary folder, and give both paths.
- In the reply, the first sentence answers the question in ASD-STE100. Then add one more sentence at most, and the offer of the next rung.
