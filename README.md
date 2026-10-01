# InternFit

ATS resume score, internship matches, a 10-week roadmap, an application tracker and Fitty, an AI coach.

## Files
- `index.html` - the whole website (CSS and JavaScript are inside it, so styles can never fail to load)
- `worker.js` - optional AI backend (Cloudflare Worker). Not uploaded to GitHub Pages; you paste it into Cloudflare
- `.nojekyll` - tells GitHub Pages to serve files as they are

## Publish the website (GitHub Pages)
1. Extract the zip. GitHub does not unzip for you.
2. On github.com click + (top right), New repository. Name it `internfit`, set Public, tick "Add a README file", Create.
3. Add file, Upload files. Drag in `index.html`, `.nojekyll` and `README.md` (the files, not the folder). Commit changes.
4. Settings, Pages. Source: Deploy from a branch. Branch: main, folder: / (root). Save.
5. Wait 1 to 2 minutes. Your site is at `https://YOUR-USERNAME.github.io/internfit/`.
6. If it looks old, hard refresh with Ctrl+Shift+R.

## Turn on the real AI (optional, about 5 minutes)
Without this, Fitty uses a built-in rule-based coach that still works. With it, Fitty is a real LLM that knows the student's score, skills and matches.
1. Get an Anthropic API key at console.anthropic.com. Usage is billed to you, so set a spending limit.
2. Sign up at cloudflare.com. Go to Workers & Pages, Create, Create Worker, name it `internfit-ai`, Deploy.
3. Click Edit code, delete the sample code, paste all of `worker.js`, Deploy.
4. Open the Worker's Settings, Variables and Secrets. Add a Secret named `ANTHROPIC_API_KEY` with your key. Add a Text variable `ALLOWED_ORIGIN` = `https://YOUR-USERNAME.github.io` so only your site can use it. Deploy.
5. Copy the Worker URL (`https://internfit-ai.YOUR-NAME.workers.dev`).
6. Easiest for all visitors: open `index.html`, find `const AI_ENDPOINT=''` near the top of the script, paste the URL between the quotes, and commit. Or, for testing, paste it in Fitty's "AI settings" box on the site.

Never put your API key in `index.html`. Anyone could read it.

## Add real internships
Listings are samples. Edit the `LIST` table in `index.html` (one line per listing: role|company|city|mode|stipend|duration). The role name must match one of the 12 role names in `JOBS`. "Find live openings" opens a real LinkedIn search for that role.

## Privacy
The resume is analysed in the browser and saved in this device's localStorage. With the AI connected, chat messages and a summary of results (score, skills, matches) are sent to your Worker and the AI provider. The full resume text is not sent.
