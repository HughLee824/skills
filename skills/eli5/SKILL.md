---
name: eli5
description: "Create a beginner-friendly visual explainer as a portable, standalone HTML file using large diagrams and minimal text. Use when the user invokes $eli5, asks for an ELI5 explanation, or requests a simple picture-based explanation of how something works. Do not use for requests that only need a brief text definition."
license: Apache-2.0
---

# ELI5

Turn the requested topic into an accurate, visual-first explanation for a reader with no prior knowledge.

## Interpret the request

- Treat the text accompanying `$eli5` and relevant conversation context as the topic. Do not expect Claude-style `$ARGUMENTS` substitution.
- Preserve the user's language, intended audience, requested scope, and output preferences.
- If no topic can be inferred, ask for it in one short question.

## Explain clearly

- Keep the underlying causal model accurate while simplifying vocabulary and detail.
- Use a friendly tone without talking down to the reader or pretending the reader is literally five unless asked.
- Prefer one concrete analogy when it improves understanding, and distinguish the analogy from the real mechanism.
- For medical, legal, financial, or safety-critical topics, retain any caveat needed to prevent a misleading or unsafe takeaway.

## Create the visual explainer

- Always create and deliver one portable, self-contained `.html` file. Invoking `$eli5` counts as an explicit request for this file; do not wait for a separate save or export request.
- An inline visualization or host artifact may be added as a preview, but it never replaces the standalone file or its final file link. Do not use an inline-only visualization workflow for the primary deliverable.
- Use the user's requested output path when provided. Otherwise use a durable, task-owned artifact location exposed by the host. Use the current project only when the request is about that project and the file clearly belongs there; never use `/tmp` or another ephemeral preview path as the delivered file.
- Write a complete HTML document containing `<!doctype html>`, `<html lang="...">`, `<head>` with UTF-8 charset, viewport metadata and a title, and `<body>`.
- Use inline CSS and inline HTML or SVG. Add a small amount of vanilla JavaScript only when interaction materially improves understanding. Avoid remote assets and build steps.
- Do not depend on host-only CSS variables, visualization directives, or APIs such as `window.openai`. Define every CSS variable used by the document, or provide a local fallback.
- Let large, simple visuals carry the explanation: diagrams, arrows, labels, short captions, and a small concrete example. Keep prose sparse and avoid walls of text.
- Choose the smallest sequence of panels that makes the idea understandable. End with a brief recap of the core idea.
- Make the result responsive and readable, with clear hierarchy, sufficient contrast, and meaningful text alternatives for instructional visuals.
- Avoid decorative complexity, unexplained jargon, and simplifications that become false.

## Verify and return

- Read back the exact delivered file and confirm it satisfies the complete-document and portability requirements above.
- When browser or rendering tools are available, open the exact delivered file, or serve that exact file without wrapping or transforming it. Check that the main idea is understandable at a glance, text is legible, interactions work, and nothing clips or overflows. Fix obvious issues and validate the same file again.
- Return a clickable link to the exact standalone HTML file. If an optional inline preview fails to render, the standalone link must still let the user read the explanation.
