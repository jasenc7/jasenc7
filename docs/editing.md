# Editing the public profile

This document is the procedure for correcting statements on the public GitHub
profile. It does not select or make any correction itself.

## Ownership and publication

- The repository owner, `jasenc7`, controls publication of every profile
  statement. Nothing reaches the profile without the owner choosing the exact
  wording.
- This repository is named after the account, so GitHub renders the root
  `README.md` directly as the account profile. There is no build step,
  generator or deployment: the Markdown on the default branch (`main`) is what
  the profile shows.
- Files elsewhere in the repository, including this one, are visible in the
  repository but are not part of the profile.

## Change record

Edit `README.md` only for a wording change the owner has actually selected.
Write the record first, then make the edit. A complete record has all of these
fields:

| Field | Content |
|---|---|
| README section | The heading the change sits under, e.g. `Selected Work`. |
| Exact old wording | The current text, copied verbatim. |
| Exact replacement wording | The new text as the owner selected it, verbatim. For a removal, state that the text is removed. |
| Reason | Why the statement changes, e.g. inaccurate, outdated, project retired. |
| Intended public link | The URL the changed text should point to, or `none`. |

The record goes in the pull request description for the change, so it stays in
the repository history next to the commit it describes. A record with any field
missing is not ready to edit from.

```markdown
- README section:
- Exact old wording:
- Exact replacement wording:
- Reason:
- Intended public link:
```

## Making the change

Use the existing Git workflow. No build, runner, package or deployment workflow
is involved.

1. Branch from `main`.
2. Change only the text named in the record. Leave the rest of the README as it
   is.
3. Commit with a message naming the section, for example
   `docs: correct Selected Work entry for <project>`.
4. Open a pull request into `main` with the change record in its description.
5. Merge. The profile shows the new text as soon as `main` contains it.

## Retired projects and links

Retiring a project or link is its own content change with its own record: the
section, the exact row or link being changed, and the replacement wording the
owner selected (or the explicit decision to remove it). It does not authorize
removing unrelated profile history, other projects, or rewriting personal
claims. Any change to a personal claim needs the owner's selected replacement
wording.

## Private material

This repository and its issues and pull requests are public.

- Keep private drafts, client details and unpublished background information out
  of issue bodies, pull request descriptions, commit messages and repository
  files.
- When a correction rests on sensitive source evidence, describe that evidence
  only in the owner's local custody record, outside this repository. The public
  change record gives the reason in general terms and does not reproduce the
  evidence.

## Recovery

Restore only what changed. Never reset the whole repository or force-push
`main`; later, unrelated profile edits and the repository history must survive.

1. Find the commit that made the change:

   ```bash
   git log -p -- README.md
   ```

2. Undo it with one of the following, on a new branch from `main`:
   - **Revert the commit** if it changed only the selected text. This keeps
     every later edit:

     ```bash
     git revert <commit>
     ```

   - **Restore individual hunks** if the commit touched more than the selected
     text. Pick only the hunks to bring back:

     ```bash
     git restore -p --source=<commit>^ README.md
     ```

3. Open a pull request with a change record whose replacement wording is the
   restored text and whose reason is the rollback, then merge it as above.

The same steps apply to this document: restore `docs/editing.md` alone,
without touching `README.md`.
