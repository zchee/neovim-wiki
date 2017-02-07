##### contributing to this list:
* [ideas page manual](http://write.flossmanuals.net/gsoc-mentoring/making-your-ideas-page/)
* [example](https://github.com/nim-lang/nim/wiki/gsoc-2016-ideas)

# introduction
below is a list of project ideas for [gsoc 2017](https://developers.google.com/open-source/gsoc/). these projects may require familiarity with c, makefiles, python, lua or vimscript.

[neovim](https://neovim.io/) is an extension of vim. the [vision](https://neovim.io/charter/) of neovim goes into the projects goals and non-goals. one of the goals is to build a project the encourages "hacking" and collaboration. effort is put into removing barriers for contributors and improving documentation. the wiki has sections on developing and contributing to help you get started working with neovim.

the neovim source has roots in 1987 which means many libraries such as [libuv](https://github.com/libuv/libuv) were not around at that time. the code base can be made easier to maintain and understand by using these libraries. project ideas that involve working heavily with internals will in the general case be more difficult than project ideas that "simply" add new features. however working with older/complex parts of the code base can also provide valuable learning feedback for writing simpler and more maintainable code. there is a large range of skills that can be learned and working with the team to find a project that will help you the most is in your benefit.

we encourage you to join the #neovim irc or [gitter channel](https://gitter.im/neovim/neovim) to discuss these projects with the community and our mentors. because communication is a big part of open source development you are expected to get in touch with us before making your application

the following list of projects are just some ideas. we are happy to hear any suggestions that you may have.

## tips 

- anywhere a vim concept (such as "textlock") is mentioned, you can find what it means by using the ":help" command (`:help textlock`).
- ask questions and post your partial work frequently (say, once every day or 2, if possible). it's ok if work is messy; just put "[wip]" in the pull request (pr) title.
- take advantage of the continuous integration (ci) systems which automatically run against your pull
requests. when you send work to a pr,  the full test-suite runs on the pr while you continue to work locally.

# projects

## table of contents
  * [refactoring](#refactoring)
      * 
      * [external ui api](#improve-external-ui-api) 

  * [new features](#new-features)
      * [lsp support](#lsp-support)
      * 

  * [tools &amp; infrastructure](#tools--infrastructure)
      * [continuous integration](#improve-continuous-integration)

## refactoring
___
#### improve external ui api

**desirable skills:**
c language, performance testing

**description:**
neovim can be embedded via it's [msgpack rpc api](https://neovim.io/doc/user/msgpack_rpc.html). there are [projects](https://github.com/neovim/neovim/wiki/related-projects) doing this for many languages already. the client holds an internal representation of the user interface which it updates following the api. clients in higher level languages can/are currently apply optimizations to improve the performance. the main performance bottle neck for such languages is scrolling which requires many value lookups per second which is hampered by [boxed values](http://stackoverflow.com/questions/13055/what-is-boxing-and-unboxing-and-what-are-the-trade-offs).

there are various ways the api could be improved:
  * optimize screen drawing instructions in `screen.c`
  * sdk for developing frontend gui's
  * api taking future [improvements](https://github.com/neovim/neovim/pull/5686) into account

**expected result:**
interfaces implemented with the external api are faster and easier to implement

**difficulty:** ...
medium to hard

**mentor:** justin m keys ([@justinmk](http://github.com/justinmk))

## new features
___
#### lsp support

**desirable skills:**

**description:**
https://github.com/neovim/neovim/issues/4982
**expected result:**

**difficulty:** ...

**mentor:** justin m keys ([@justinmk](http://github.com/justinmk))

## tools & infrastructure

___
#### improve continuous integration

**desirable skills:**
familiarity with command line

**description:**
https://github.com/neovim/bot-ci/issues/12

**expected result:**

**difficulty:** ...
easy

**mentor:** justin m keys ([@justinmk](http://github.com/justinmk))



please add your project ideas in the following format.

# project spec

## sub-project
___
#### title

**desirable skills:**

**description:**

**expected result:**

**difficulty:** ...

**mentor:** mentor name ([@mentorname](http://github.com/mentorname))
