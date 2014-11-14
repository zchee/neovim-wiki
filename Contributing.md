## Thank you

Thanks for considering contributing to Neovim.

## What needs to be done

- [Entry-level issues](https://github.com/neovim/neovim/labels/entry-level)
- [Code reviews](https://github.com/neovim/neovim/pulls) [![PRs waiting for review](https://badge.waffle.io/neovim/neovim.png?label=RFC&title=RFC)](https://waffle.io/neovim/neovim)
- [Port OS layer to libuv](Porting-OS-layer-to-libuv)
- [Merge patches from upstream Vim](Merging-patches-from-upstream-vim)

Check this [refactoring catalog](https://github.com/neovim/neovim/wiki/C-Refactorings-and-Code-Smells-Catalog) if you want some inspiration on what to work on.

## Pull Requests

See [CONTRIBUTING.md](https://github.com/neovim/neovim/blob/master/CONTRIBUTING.md#pull-requests)
for guidelines on sending contributions as pull requests.

## Coverity

[Coverity Scan](https://scan.coverity.com/) is used to detect defects in the
code. Check out the [Neovim Coverity](https://scan.coverity.com/projects/2227)
project to see the info on the latest build.

If you want to see the defects and fix them, you need to request access at the
**Contributor** level. An Admin will grant you permission as soon as they are
able. If you join as an **Observer/User**, you won't get to see the defects,
it'll just add Neovim to your [Dashboard](https://scan.coverity.com/dashboard).

### Coverity Conventions

If you decide to fix a Coverity defect, follow this convention for your commit messages when you issue the pull request:
```
coverity/<id>: <description of what fixed the defect>
```

where `<id>` is the Coverity ID. The id is also called the CID. For an example, take a look at [Issue #804](https://github.com/neovim/neovim/pull/804).

## Non-programming ways to contribute

There is plenty of stuff you can contribute without being a hardcore C programmer.

### Use Neovim
Use Neovim, and report bugs on this GitHub page.

### Give support
Hang around the irc channel #neovim at FreeNode and answer questions.

### Documentation
Help document Neovim by editing this wiki or making pull requests for [`runtime/doc/`](https://github.com/neovim/neovim/tree/master/runtime/doc).

### Raise awareness
Write about Neovim and show it to your friends

### Money contributions
Consider spending your hard-earned cash wisely: https://www.bountysource.com/fundraisers/539-neovim-first-iteration

### Help manage the issue tracker
If you spot a duplicate issue, flag it up with a comment. If you see a report lacking in detail, ask for more.

## Help with contributing

See [Communicating](Communicating). Raise documentation issues.
