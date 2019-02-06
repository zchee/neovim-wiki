# GSoC 2019 ideas

#### Contributing to this list:

* [Ideas page Manual](http://write.flossmanuals.net/gsoc-mentoring/making-your-ideas-page/)
* [Example](https://github.com/nim-lang/Nim/wiki/GSoC-2016-Ideas)

# Introduction
Below is a list of project ideas for [Google Summer of Code](https://developers.google.com/open-source/gsoc/). These projects may require familiarity with C, Makefiles, Python, Lua or vimscript.

[Neovim](https://neovim.io/) is an extension of Vim. One of the [project goals](https://neovim.io/charter/) is to build a project that encourages "hacking" and collaboration. Effort is put into removing barriers for contributors and improving documentation. The wiki has sections on developing and contributing to help you get started.

The Neovim source has roots going back to 1987 which means many libraries such as [libuv](https://github.com/libuv/libuv) were not around at that time. The code base can be made easier to maintain and understand by using these libraries. Project ideas that involve working heavily with internals will in general be more difficult than project ideas that "simply" add new features. However working with older/complex parts of the code base can also provide valuable learning feedback for writing simpler and more maintainable code. There is a large range of skills that can be learned and working with the team to find a project that will help you the most is in your benefit.

We encourage you to join the `#neovim` IRC or [gitter channel](https://gitter.im/neovim/neovim) to discuss these projects with the community and our mentors. Because communication is a big part of open source development you are expected to get in touch with us before making your application.

It's also recommended to start with a smaller coding task, to get introduced to the Neovim project. Look on the issue tracker for simpler issues and submit a small PR attempting to solve the issue. See for instance the [good first issue](https://github.com/neovim/neovim/issues?utf8=✓&q=is%3Aopen+is%3Aissue+label%3A"good+first+issue") and [complexity:low](https://github.com/neovim/neovim/issues?q=is%3Aopen+is%3Aissue+label%3Acomplexity%3Alow) tags. The goal here is to get accustomed with the codebase and to our workflow for reviewing and testing PRs, rather than directly making a large code contribution.

The following list of projects are just some ideas. We are happy to hear any suggestions that you may have.

## Making a proposal

The application period for GSOC is March 12-27. Send your proposal through the official [GSOC page](https://summerofcode.withgoogle.com/organizations/6156058456752128/). We encourage students to send a first draft early in this period, this allows us to give feedback and and ask for more information if need. See https://google.github.io/gsocguides/student/writing-a-proposal for some guidelines for writing a good proposal. 

Note: this year we will likely be able to accept two students at maximum. We expect to get more strong proposals than available slots, so we will need to turn some good proposals down.

## Proposal evaluation

Proposal evaluation criteria:

http://intermine.org/gsoc/guidance/grading-criteria/



## Tips 

- Anywhere a Vim concept (such as "textlock") is mentioned, you can find what it means by using the ":help" command from within neovim (`:help textlock`).
- Ask questions and post your partial work frequently (say, once every day or 2, if possible). It's OK if work is messy; just put "[WIP]" in the pull request (PR) title.
- Take advantage of the continuous integration (CI) systems which automatically run against your pull
requests. When you send work to a PR,  the full test-suite runs on the PR while you continue to work locally.
- The [wiki](https://github.com/neovim/neovim/wiki) contains up-to-date documentation on building, debugging, and development tips.
- Only a text editor, cmake, and a compiler are needed to develop Neovim. [ctags](https://github.com/universal-ctags/ctags) is very helpful also.
- The [contributing guidelines](https://github.com/neovim/neovim/blob/master/CONTRIBUTING.md) are intended to be
helpful, not rigid.

# Projects

## Table of Contents

  * [New Features](#new-features)
      * ["multiprocessing" feature](#multiprocessing-feature)
      * [TUI client](#tui-terminal-ui-remote-attachment)
      * [Live preview of commands](#live-preview-of-commands)
      * [Improve autoread](#improve-autoread)

## New Features
___
#### "multiprocessing" feature

**Desirable Skills:**

* Experience with concurrency and interprocess communication
* Strong experience with C
* Familiar with VimL (Vim script) and Vim concepts (quickfix list, buffers, etc.)

**Description:**

p2p architecture for data sharing between multiple nvim instances. Similar to Python's [multiprocessing](https://docs.python.org/3/library/multiprocessing.html) module, the idea is to to offload Nvim tasks (VimL and/or Lua) to child Nvim processes.

**Difficulty:** Hard

**Mentor:** Justin M Keyes ([@justinmk](http://github.com/justinmk))

___

#### TUI (Terminal UI) remote attachment

**Desirable Skills:**

C

**Description:**

The built-in UI is called the TUI. It looks like Vim, but internally it is decoupled from the UI and "screen" layout subsystem. It was designed to be able to connect to other (remote) instances of Nvim, but this hasn't been implemented yet. [#7438](https://github.com/neovim/neovim/issues/7438)

**Expected Result:**

Modify the TUI subsystem so that it can display a remote Nvim instance.

Example:

    nvim --servername foo

will connect to the Nvim server at address `foo`. The `nvim` client instance sends input to the remote Nvim server, and reflects the UI of the remote Nvim server. So the `nvim` client acts like any other external (G)UI.

- Code license: Apache 2.0

**Difficulty:** 

Medium

**Mentor:** Justin M Keyes ([@justinmk](http://github.com/justinmk))

___
#### Live preview of commands

**Desirable Skills:**

- C and related tools
- Familiar with event-loop programming model

**Description:**

Nvim has builtin live preview of `:%s` substitution, as a result of a [[successful collaboration with students|https://medium.com/@eric.burel/stop-using-open-source-5cb19baca44d]]. This support could be extended to more commands, such as `:global` and `:normal`.

**Expected Result:**

More commands support interactive preview. This could be done by extending the hard-coded support for substitution preview to more commands. Alternatively, a more scalable approach could be to add core functionality that makes it easier to implement live preview as plugins in vimL and/or lua. See [[#7370|https://github.com/neovim/neovim/issues/7370]] for some ideas.

- Code license: Apache 2.0

**Difficulty:**

Medium

**Mentor:** Björn Linse ([@bfredl](http://github.com/bfredl))

---

#### Improve autoread

**Desirable:** Any  

**Description:** Reload file/notify user when a file being edited changes outside of `nvim`. 

**Expected Result:**

Neovim has the 'autoread' setting that regularly checks if a file edited in neovim has been externally modified. It thus notifies the user to prevent overwriting the changes. Sadly the current mechanism isn't foolproof. This project intends to make this feature work as well as in other editors like Sublime text and across the neovim supported platforms. The interface should also be improved so that notifications show how different the edited and modified files are. 
The candidate can realize some of the difficulties involved with this [proposition for linux](https://github.com/neovim/neovim/issues/1380)

- Code license: Apache 2.0

**Difficulty:** Medium

**Mentor:** Matthieu Coudron ([@teto](http://github.com/teto))
___
#### Neovim-based "Vim mode"

**Desirable:** Any  

**Description:** Implement "Vim mode" in an editor/IDE (such as IntelliJ) by embedding a `nvim` instance. 

**Expected Result:**

Full Nvim editing should be available in the editor/IDE, while also allowing the user to use the native editor/IDE features.

- Code license: Apache 2.0

Examples:

- [VSCode integration](https://github.com/VSCodeVim/Vim)
- [Sublime Text integration](https://github.com/lunixbochs/actualvim)

**Difficulty:** Medium (maybe Easy, depending on the extensiveness of the emulation)

**Mentor:** Horace He ([@chillee](http://github.com/chillee))


___

Please add your project ideas in the following format.

# Project spec

## Sub-project
___
#### Title

**Desirable Skills:**

**Description:**

**Expected Result:**

- Item1
- Item2
- Code license: Apache 2.0

**Difficulty:** 

**Mentor:** Mentor name ([@MentorName](http://github.com/MentorName))