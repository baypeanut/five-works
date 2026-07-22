# Noah Dericioglu — Six Works (curatedengineer.com)

An exhibition-catalogue portfolio. Six works presented as a fanned deck of
flippable catalogue plates, plus an "Ask the desk" assistant that answers
visitor questions about Noah's work.

## Structure
- `index.html` — the static catalogue (self-contained: deck, checklist, chat UI).
- `api/chat.ts` — Vercel Edge function that streams answers from Claude
  (`claude-haiku-4-5`), grounded only in Noah's portfolio and scoped to
  questions about him.
- `package.json` — declares `@anthropic-ai/sdk`.

## Deploy / configure
The assistant needs one environment variable in Vercel:

    ANTHROPIC_API_KEY = <your Anthropic API key>

Set it in the Vercel dashboard (Project → Settings → Environment Variables),
then redeploy. Until it is set, the deck and site work; the chat returns a
"not configured yet" notice.
