# curatedengineer.com

Personal portfolio for Noah Dericioglu, built as an exhibition catalogue. Six
projects are presented as a deck of catalogue plates you turn over to read,
next to "Ask the desk": an assistant, backed by Claude, that answers questions
about the work.

Live at **[curatedengineer.com](https://curatedengineer.com)**.

## The assistant

The chat panel is the part of this repository worth reading the code for. It is
a Vercel Edge Function that streams responses from the Anthropic API, with its
constraints built in rather than added afterwards.

**Grounded.** The system prompt carries a fixed, hand-written brief covering
each project. The model answers only from that brief and is instructed never to
invent a figure, a date, or a credential it was not given. Anything the brief
does not cover is answered with a referral to email rather than a guess.

**Scoped.** Questions outside the subject are declined and redirected, and
instructions embedded in visitor input cannot widen that scope.

**Rendered as text, never as markup.** Model output reaches the DOM through
`textContent`, so a response can never inject HTML into the page. Output is also
normalized server-side so formatting intended for a markdown renderer does not
surface as stray characters in a plain-text interface.

The function calls the REST API with `fetch` rather than the official SDK,
because the SDK depends on Node built-ins (`node:fs`, `node:path`) that the Edge
runtime rejects.

## Structure

| Path | Purpose |
| --- | --- |
| `index.html` | The entire front end: catalogue deck, checklist, and chat interface. No build step, no framework, no external assets. |
| `api/chat.ts` | The Edge Function backing the assistant, including the grounding brief. |
| `vercel.json` | Deployment configuration. |

## Running it

The site itself is static, so `index.html` can be opened directly in a browser.

The assistant needs an Anthropic API key available to the deployment:

```
ANTHROPIC_API_KEY=<key>
```

Set it in the Vercel project settings and redeploy, since the function reads the
key at deploy time. Without the key the site serves normally and the assistant
reports that it is not configured.
