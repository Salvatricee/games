# Contributing — build your game

Welcome! Each student builds **one game**, entirely inside its own folder, and ships it
through a real pull request. This is exactly how teams work in industry: claim a task,
branch, build, open a PR, get it reviewed, merge.

## The workflow

### 1. Claim a game

- Browse the [open game issues](../../issues). Each issue is the full spec for one game.
- Find one labelled **`unclaimed`** for **your class** (`ada-lab` or `anita-b`) that you like.
- **Comment `claiming` on the issue.** Your instructor will confirm and mark it `claimed` so
  nobody doubles up. Wait for that confirmation before you start building.

> Why comment instead of assigning yourself? Assigning issues and changing labels needs
> special repo access that students don't have — commenting is the claim, and your instructor
> does the labelling.

### 2. Fork the repository

A **fork** is your own personal copy of the project, living under your GitHub account. You
have full control of your fork; you build your game there and then propose your work back to
the class repo with a pull request. You don't need any special access to the class repo to do
this — that's the whole point of a fork.

- Open the class repo on GitHub and click **Fork** (top-right).
- This creates `https://github.com/<your-username>/games` — your copy.

### 3. Clone your fork & set up (once)

Clone **your fork** (not the class repo) and install dependencies:

```bash
git clone https://github.com/<your-username>/games.git
cd games
npm install
npm run dev        # open http://localhost:3000
```

Add the class repo as a second remote called `upstream` so you can pull in others' merged
games later:

```bash
git remote add upstream https://github.com/mainawycliffe/games.git
git remote -v      # origin = your fork, upstream = the class repo
```

### 4. Create a branch

```bash
git checkout -b <your-slug>      # e.g. git checkout -b snake
```

### 5. Build your game

- Your folder already exists as a placeholder: **`app/games/<your-slug>/`**.
- Replace `page.jsx` in that folder with your game. Update `meta.js`.
- **Only touch files inside your own folder.** This is what keeps 50+ people working in
  one repo without conflicts — and it's the first thing the reviewer checks.
- Look at **`app/games/tic-tac-toe/`** for a complete example: it splits pure game rules
  (`logic.js`) from the UI (`page.jsx`) and has tests (`game.test.jsx`). Copy that shape.
- Use the shared UI kit in `components/ui/` (shadcn) — `Button`, `Card`, `Badge`, etc.

### 6. Fill in `meta.js`

```js
const meta = {
  title: "Snake",
  difficulty: "medium",
  issue: 23,
  status: "done", // <- flip from "unclaimed" to "done" when it's playable
  author: "Your Name",
  github: "yourhandle",
  description: "Eat, grow, and don't hit your own tail.",
};
export default meta;
```

Setting `status: "done"` makes your card on the homepage link to your playable game.

### 7. Check everything passes locally

CI will run these on your PR — run them first so there are no surprises:

```bash
npm run format:check   # formatting (fix with: npm run format)
npm run lint           # linting
npm run build          # production build — a broken game fails here
```

### 8. Push to your fork & open a pull request

Commit your work and push the branch to **your fork** (`origin`):

```bash
git add app/games/<your-slug>
git commit -m "Add <game> game"
git push -u origin <your-slug>
```

Now go to the class repo on GitHub — it will show a **"Compare & pull request"** button for
your branch. Open the PR **from your fork's branch into the class repo's `main`**. In the
description write **`Closes #<your-issue-number>`** so your game issue closes automatically
when it merges. A **Vercel preview link** appears on the PR — click it to play your game live,
and paste it into the PR description.

### 9. Review & merge

Your instructor reviews the PR. Once approved and all checks are green, it's merged and your
game goes live on the arcade. 🎉

## Rules of thumb

- **One folder per person.** Never edit another game's folder or a shared file.
- **Keep it self-contained.** Everything your game needs lives in your folder (except the
  shared `components/ui` kit).
- **Ask for help early** — in the issue comments or with your instructor.
