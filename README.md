# curatedengineer.com

My portfolio, built as an exhibition catalogue: each project is a card you turn
over to read. It also has a small assistant, backed by Claude, that answers
questions about the work.

Live at [curatedengineer.com](https://curatedengineer.com).

### Built with

Plain HTML, CSS and JavaScript on the front end, no framework and no build step.
The assistant is a Vercel Edge Function calling the Anthropic API, and needs
`ANTHROPIC_API_KEY` set in the Vercel environment.
