# Scoped commit messages

Use this default when repository instructions and Git hooks do not specify a
commit style. Adapted from `~/.config/AGENTS.md` (`git/commit-style.md`).

```text
<scope>: <description>
```

- The scope names the area the change touches: a directory or file that exists
  in the repository, at any depth, without extension, and always lowercase,
  even when the file name is not (`fish`, `nvim`, `bootstrap` for
  `bin/bootstrap`, `brewfile` for `Brewfile`, `readme` for `README.md`). Nest
  with `/` (`fish/conf.d`), name two areas with `, ` (`fish, nvim`), and use
  `treewide` for repository-wide changes.
- No type words: not `feat(fish):`, not `chore:`. Older history may use
  Conventional Commits (`type(scope): ...`); do not copy it for this style.
- The description is imperative ("add", not "added" or "adds"), starts with a
  lowercase word, and has no trailing period. Later words keep their case.
- The whole subject is at most 72 characters, including the scope, colon,
  and space.
- Add a body only when the reason for the change is not clear from the subject.
  Use plain prose or short bullets after a blank line.
- Trailers such as Co-Authored-By or Signed-off-by go last, after another
  blank line, when required.
- Merge, revert, and fixup!/squash!/amend! subjects that Git writes pass as-is.

## Examples

These examples assume the named files or directories exist in the repository.

- Good: `fish: add tmux sessionizer keybind`
- Good: `fish/conf.d: cache zoxide init output`
- Good: `bootstrap: install native arm64 steam instead of the intel cask`
- Good: `brewfile: add the zed cask and sort Brewfile`
- Good: `fish, nvim: switch both to the gruvbox theme`
- Good: `treewide: drop zig tooling`
- Bad: `feat(fish): add tmux sessionizer keybind` (type word)
- Bad: `chore: prune gitignore entries` (`chore` is not a path; use `gitignore:`)
- Bad: `Brewfile, fish: add direnv` (scopes are lowercase: `brewfile, fish:`)
- Bad: `fish: Added a keybind.` (capitalized, past tense, trailing period)
