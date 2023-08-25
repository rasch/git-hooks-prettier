# git-hooks-prettier

These scripts are adapted from the [shell script option for using a pre-commit
hook with Prettier][1] in the [Prettier][2] docs.

To use these hooks, place them in the repository's `.git/hooks/` directory. They
can also be used as a plugins by running [this git-hooks script][3] to set up
symlinks for each git hook and then cloning the repository to one of the
following directories:

- ~/.config/git/hooks/plugins/git-hooks-prettier (for global plugins)
- .git/hooks/git-hooks-prettier (for local plugins)
- .githooks/git-hooks-prettier (for local plugins that can be committed)

Note: This hook requires `prettier` to be installed at
`.node_modules/.bin/prettier` relative to the root of the Git repository.

Note: This hook writes to all staged files that `prettier` formats and re-adds
them to the staging area. I'm not a fan of letting a third-party rewrite code
automatically before it is checked into the repository. I've had problems in the
past (with Prettier) where poorly formatted code ended up as an empty file. I
would have preferred to use the `--check` option instead of `--write`, but it
was too error prone. The `pre-hook` (when using `--check`) would fail, then the
files would have to be formatted manually. Now the `pre-hook` would pass even
if the properly formatted files weren't re-added before commiting.

[1]: https://prettier.io/docs/en/precommit.html#option-6-shell-script
[2]: https://prettier.io/
[3]: https://git.sr.ht/~rasch/containers/blob/main/git/scripts/git-hooks
