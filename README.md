# Noah Dericioglu Portfolio (curatedengineer.com)

An exhibition-catalogue portfolio. Projects presented as a fanned deck of
flippable catalogue plates, plus an "Ask the desk" assistant that answers
visitor questions about Noah's work.

## Structure

- `index.html` is the whole static catalogue, self-contained: deck, checklist,
  and chat UI, with no build step and no external assets.
- `api/chat.ts` is a Vercel Edge function that streams answers from Claude
  (`claude-haiku-4-5`), grounded only in a fixed brief about Noah's work and
  scoped to questions about him. It calls the Anthropic REST API with `fetch`
  rather than the SDK, because the SDK pulls in Node built-ins that the Edge
  runtime rejects.
- `package.json` carries no dependencies; it exists so Vercel treats this as a
  project rather than a bare static directory.

## Deploy and configure

The assistant needs one environment variable in Vercel:

    ANTHROPIC_API_KEY = <your Anthropic API key>

Set it under Project, then Settings, then Environment Variables, and redeploy
(the function reads the key at deploy time). Until it is set, the site and the
deck work normally and the chat returns a "not configured yet" notice.

Removing the variable and redeploying cleanly disables the assistant without
affecting the rest of the site.
