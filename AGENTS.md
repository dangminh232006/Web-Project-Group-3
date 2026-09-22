# GitHub Account and Attribution

This repository belongs to GitHub account `dangminh232006`.

- Perform authenticated GitHub operations only with the stored credential for `dangminh232006`, verified through `gh api user`. Never switch the globally active GitHub account or change global Git identity.
- Use repository-local commit identity `Bui Dang Minh - 105716425 <212895881+dangminh232006@users.noreply.github.com>` for this account's commits.
- Do not add Claude or Anthropic as an author, committer, coauthor, or signatory. Do not add Claude-generated attribution text or Claude session links to commits or pull requests.
- Preserve attribution to real human contributors. Do not remove existing human authorship or silently rewrite published history.
- Keep `.claude/settings.json` attribution disabled. The tracked `.githooks/commit-msg` validates author/committer identities and rejects prohibited attribution trailers.
- This checkout installs guards through `.git/hooks/commit-msg` and `.git/hooks/pre-push`. The pre-push guard scans every commit reachable from each outgoing ref, including commits imported by rebase or cherry-pick. Git does not copy hooks to fresh clones: install or chain both tracked guards before creating commits in a new checkout, preserving existing hooks.
- Local hooks protect against accidental attribution and can be bypassed; they are not a server-side access-control boundary.
