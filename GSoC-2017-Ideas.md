##### Contributing to this list:
* [Ideas page Manual](http://write.flossmanuals.net/gsoc-mentoring/making-your-ideas-page/)
* [Example](https://github.com/nim-lang/Nim/wiki/GSoC-2016-Ideas)

# Introduction
Below is a list of project ideas for [GSoC 2017](https://developers.google.com/open-source/gsoc/). These projects may require familiarity with C, Makefiles, Python, Lua or vimscript.

[Neovim](https://neovim.io/) is an extension of Vim. The [vision](https://neovim.io/charter/) of Neovim goes into the Projects goals and non-goals. One of the goals is to build a project that encourages "hacking" and collaboration. Effort is put into removing barriers for contributors and improving documentation. The wiki has sections on developing and contributing to help you get started working with Neovim.

The Neovim source has roots going back to 1987 which means many libraries such as [libuv](https://github.com/libuv/libuv) were not around at that time. The code base can be made easier to maintain and understand by using these libraries. Project ideas that involve working heavily with internals will in general be more difficult than project ideas that "simply" add new features. However working with older/complex parts of the code base can also provide valuable learning feedback for writing simpler and more maintainable code. There is a large range of skills that can be learned and working with the team to find a project that will help you the most is in your benefit.

We encourage you to join the #neovim IRC or [gitter channel](https://gitter.im/neovim/neovim) to discuss these projects with the community and our mentors. Because communication is a big part of open source development you are expected to get in touch with us before making your application.

The following list of projects are just some ideas. We are happy to hear any suggestions that you may have.

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
  * [Refactoring](#refactoring)
      * [External UI API](#improve-external-ui-api) 

  * [New Features](#new-features)
      * ["multiprocessing" feature](#"multiprocessing"-feature)
      * [Vim perl plugin compatibility](#if_perl-compatibility-layer)
      * [Haxe client](#haxe-client)
      * [LSP support](#lsp-support)

  * [Tools &amp; Infrastructure](#tools--infrastructure)
      * [Continuous Integration](#improve-continuous-integration)
      * [Plugin Tools](#plugin-tools)
      * [Benchmarking](#benchmarking)

## Refactoring
___
#### Improve External UI API

**Desirable Skills:**
C language

**Description:**
Neovim can be embedded via it's [msgpack rpc api](https://neovim.io/doc/user/msgpack_rpc.html). There are [projects](https://github.com/neovim/neovim/wiki/Related-projects) doing this for many languages already. The client holds an internal representation of the user interface which it updates following the api. Clients in higher level languages can/are currently apply optimizations to improve the performance. The main performance bottle neck for such languages is scrolling which requires many value lookups per second which is hampered by [boxed values](http://stackoverflow.com/questions/13055/what-is-boxing-and-unboxing-and-what-are-the-trade-offs).

There are various ways the api could be improved:
  * Optimize screen drawing instructions in `screen.c`
  * A SDK for developing frontend gui's
  * Api taking future [improvements](https://github.com/neovim/neovim/pull/5686) into account

**Expected Result:**
Interfaces implemented with the external api are faster and easier to implement

**Difficulty:** ...
Medium to Hard

**Mentor:** Justin M Keyes ([@justinmk](http://github.com/justinmk))

## New Features
___
#### "multiprocessing" feature

**Desirable Skills:**
Experience with concurrency type problems and networking

**Description:**

p2p architecture for data sharing between multiple nvim instances. Similar to the "multiprocessing" module of python, the idea is to to offload Nvim computations (VimL and/or Lua) to child Nvim processes.

**Difficulty:** Medium to Hard

**Mentor:** Justin M Keyes ([@justinmk](http://github.com/justinmk))
___
#### if_perl compatibility layer

**Desirable Skills:**
any(lua, perl, python)

**Description:**

Implement Vim's legacy perl API. See the [ruby layer](https://github.com/alexgenco/neovim-ruby) for example. Vim can be compiled to support python/lua/ruby/perl plugins. Neovim has a rpc plugin architecture that allows plugins
to be written in any language. A perl api client already exists, the only part missing is a neovim plugin that works in the same way as vim perl support.

**Difficulty:** Medium to Hard

**Expected Result:** Vim perl plugins can be run in neovim.

**Mentor:** Justin M Keyes ([@justinmk](http://github.com/justinmk))

___
#### Haxe client

**Desirable Skills:**
Haxe or something object oriented Java/C#/Python/JS

**Description:**
An [api client](#https://neovim.io/doc/user/msgpack_rpc.html#rpc-api-client) written in haxe would enable more languages to have a maintained client. 

**Expected Result:**
Most tests from the current [python-client](https://github.com/neovim/python-client) are passable by the haxe python client.

**Difficulty:**
medium

**Mentor:** Justin M Keyes ([@justinmk](http://github.com/justinmk))
___
#### LSP support

**Desirable Skills:**

**Description:**
[initial discussion](https://github.com/neovim/neovim/issues/4982)
continued [here](https://github.com/neovim/neovim/issues/5522)

**Expected Result:**

**Difficulty:**

**Mentor:** Justin M Keyes ([@justinmk](http://github.com/justinmk))

## Tools & Infrastructure

___
#### Improve Continuous Integration

**Desirable Skills:**
Familiarity with command line

**Description:**
Automating builds and other tasks lowers the obstacles for contributors. Tasks include automatically pushing build artifacts to github releases, html document generation, rewriting some awk scripts to python, clang tidy builds. See [Neovim/bot-ci repo](https://github.com/neovim/bot-ci)

**Difficulty:**
Easy

**Mentor:** Justin M Keyes ([@justinmk](http://github.com/justinmk))
___
#### Plugin tools

**Desirable Skills:**
A good prototyping language.

**Description:**
Neovim plugin tools can be developed for multiple user types. For regular users the
`:CheckHealth` command could be improved to detect clashes or missing requirements
of plugins.
Users looking to embed neovim into application could make use of an sdk to 
build an Intellij like Plugin Manager.

**Difficulty:**
easy to Hard

**Mentor:** Justin M Keyes ([@justinmk](http://github.com/justinmk))

___
#### Benchmarking

**Desirable Skills:**
Experience with benchmarking, ability to create modern websites.

**Description:**
With an ever changing code base it can be easy to miss regressions
in performance. A tool for easily creating benchmarks
for time, memory usage, utilization of each CPU core or compilation times can be
interesting metrics to have.

**Difficulty:**
easy to medium

**Mentor:** Justin M Keyes ([@justinmk](http://github.com/justinmk))


Please add your project ideas in the following format.

# Project spec

## Sub-project
___
#### Title

**Desirable Skills:**

**Description:**

**Expected Result:**

**Difficulty:** 

**Mentor:** Mentor name ([@MentorName](http://github.com/MentorName))