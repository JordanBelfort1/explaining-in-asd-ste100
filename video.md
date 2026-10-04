# Explainer video

Prompt that works: "Make an explainer video in the style of 3Blue1Brown about X. Use my ElevenLabs key for the narration."

## Pick the engine

| Engine | Use for | Notes |
|---|---|---|
| Manim Community (Python, `pip install manim`) | 3b1b style: math, algorithms, protocols, data that moves | `MathTex` needs a LaTeX install. Use `Text` when you have no LaTeX. |
| Remotion (React) | Product and UI explainers, real screenshots, brand type | If the repo already has a Remotion project (e.g. `promo-video/`), use that pipeline. |

## Pick the voice

| Voice | Cost | Languages |
|---|---|---|
| ElevenLabs API | Paid, billed per character | Many, including PL and ES |
| Piper (`pip install piper-tts`) | Free, runs on the local CPU | Many, including PL (`pl_PL-*` voices) and ES |
| Kokoro-82M (`pip install kokoro`) | Free, local | EN, ES, FR, IT, PT, JA, ZH, HI, but not PL |

Read the ElevenLabs key from `ELEVENLABS_API_KEY` in a gitignored `.env`. Never print the key, write it into a file or put it in a commit. If you have no key, offer Piper or Kokoro.

## Steps

1. **Script.** Write the narration in ASD-STE100 (see SKILL.md), 60–180 s. One scene = one idea. List the scenes with the picture for each one.
2. **Audio first.** Generate the narration for each scene and measure the durations.
3. **Animate to the audio.** Each scene lasts as long as its narration. The picture changes when the narration names the thing.
4. **Render** to a gitignored folder (e.g. `artifacts/video/`).
5. **Check before showing.** Look at frames around every cut, for example on a contact sheet. Look for text off-screen, overlaps and wrong order.
6. **Hand over** the path to the file, the length, and how to change the script and render again.
