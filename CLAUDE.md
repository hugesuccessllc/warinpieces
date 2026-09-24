# CLAUDE.md

Rules for Claude when working in this repository. These are hard rules, not suggestions.

## 1. Git is read-only

- NEVER run `git commit`, `git add`, `git rm`, `git merge`, or any other command that writes to the index, the working tree via git, refs, or history.
- That includes (but is not limited to): `rebase`, `reset`, `revert`, `cherry-pick`, `stash`, `checkout`/`switch`/`restore` that change files, `branch`/`tag` creation or deletion, `push`, `pull`, `fetch` into refs, `commit --amend`, `filter-branch`, `gc`, `clean`, and editing anything under `.git/`.
- Read-only commands are fine: `git status`, `git log`, `git diff`, `git show`, `git blame`, `git branch --list`, etc.
- All git writes are for the human operator alone. If a task seems to need one, stop and tell the operator what to run.

## 2. Stay inside this repository

- Do not read or write any file outside this project repo (`~/git/warinpieces`) unless the human operator EXPLICITLY authorizes that specific access.
- This includes reads (e.g. `~/.config`, other projects, `/etc`) and writes (e.g. `/tmp`, home directory dotfiles). No `cd ..` excursions, no absolute paths elsewhere, no following symlinks out of the tree.
- Authorization for one outside path does not extend to others, or to later tasks.

## 3. Tooling is written in Ruby

- Where possible, write tooling/scripts in Ruby.
- Code must be compatible with standard Ruby 3.3.8. Avoid features introduced after 3.3 (e.g. the `it` block parameter from 3.4).
- Prefer the Ruby standard library. Do not assume third-party gems are available (see rule 4).

## 4. Never install software

- NEVER install software by any means: `brew`, `npm`/`npx`/`yarn`/`pnpm`, `gem install`, `bundle install`, `pip`/`pipx`, `cargo`, `go install`, `curl | sh`, downloading binaries, etc.
- If a needed tool, gem, or library is missing: HALT the current task and ask the human operator to consider installing it themselves, manually. Explain what is missing and why it's needed, and suggest alternatives that use only what is already installed.