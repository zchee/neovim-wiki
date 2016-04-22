## Relevant vim patches before 7.4.1000

List of patches before 7.4.1000 that are neither merged nor declared NA. Currently, the content of this page refers to 

https://github.com/neovim/neovim/tree/ba9bdb3e70722942049fc17c52ef3d9eea866256.

### Tagged patches

|Tag|  Ongoing work| Comment|
|---|-------------|--------|
|[7.4.238](https://github.com/vim/vim/commit/5bd32f47ec5121a5485d180add1dacb73472e4b2)|---| Support for [smack library](https://en.wikipedia.org/wiki/Smack_%28Linux_security_module%29)|
|[7.4.244](https://github.com/vim/vim/commit/57a728d1df7451f5b2b6b1f933182b5af9513d83)|---| Smack support fixes|
|---| https://github.com/neovim/neovim/pull/4301  | Marks smack support as NA |
|[7.4.613](https://github.com/vim/vim/commit/70781ee)|https://github.com/neovim/neovim/pull/4070| Implement redrawtime for nfa engine|
| | https://github.com/neovim/neovim/pull/4630||
|| Related| https://github.com/vim/vim/commit/5ad075c|
|| Related|https://github.com/vim/vim/commit/7c29f38|
|| Related|https://github.com/vim/vim/commit/2a6fa56|
|[7.4.672](https://github.com/vim/vim/commit/b5971141dff0c69355fd64196fcc0d0d071d4c82)|---| Always look in current dir for shell completion|
|[7.4.733](https://github.com/vim/vim/commit/d68f2219b57acb86ddedebdcc1476fee15c9c0c7)|---| test_listchars on windows|
|[7.4.797](https://github.com/vim/vim/commit/5f95f288a2d303be1571e818655fd90e399ee58e)|See [below](### Comments/Research on specific patches)| Crash @ command line|
|[7.4.822](https://github.com/vim/vim/commit/cde885473099296c4837de261833f48b24caf87c)|---| Silence coverity warnings|
[7.4.871](https://github.com/vim/vim/commit/7b256fe7445b46929f660ea74e9090418f857696)|---| Fix memory leak|
|[7.4.882](https://github.com/vim/vim/commit/5f1fea28f5bc573e2430773c49e95ae1f9cc2a25)|---| Screen update @CTRL-C with compl-menu|
|[7.4.889](https://github.com/vim/vim/commit/74b738d414b2895b3365e26ae3b7792eb82ccf47)|---| Test triggering OptionSet from setwinvar|
|[7.4.896](https://github.com/vim/vim/commit/b4f6a46b01ed00b642a2271e9d1559e51ab0f2c4)|---| Editing URL & netrw|
|[7.4.941](https://github.com/vim/vim/commit/bc96c29ffc753daef302d20322d1e3d560094f44)|https://github.com/neovim/neovim/pull/4273|add tagcase option|
|[7.4.942](https://github.com/vim/vim/commit/60422e68a3a555144f8c76c666f050e8d104c16b)|https://github.com/neovim/neovim/pull/4273|test_tagcase fix|
|[7.4.951](https://github.com/vim/vim/commit/b00da1d6d1655cb6e415f84ecc3be5ff3b790811)|https://github.com/neovim/neovim/pull/4303| Add N argument to sort|
|[7.4.957](https://github.com/vim/vim/commit/bc96c29ffc753daef302d20322d1e3d560094f44)|https://github.com/neovim/neovim/pull/4273| test_tagcase fix|
|[7.4.983](https://github.com/vim/vim/commit/a60824308cd9bc192c5d38fc16cccfcf652b40f6)|---| Make testclean fix|
|[7.4.984](https://github.com/vim/vim/commit/ad4d8a192abf44b89371af87d70b971cd654b799)|https://github.com/neovim/neovim/pull/4325| Add z flag  for searchpos|
|[7.4.998](https://github.com/vim/vim/commit/f9c8bd2137b045f9a64d63eefcf022b4726b1419)|---| Test in shadow dir fix|

### Untagged patches

All are for runtime files, in merge order:

* https://github.com/vim/vim/commit/a0f849ee40cbea3c889345256786b640b0becca2
* https://github.com/vim/vim/commit/d7464be9747fcaa8e6210e1f00a3882932df76e2
* https://github.com/vim/vim/commit/b4ff518d95aa57c2f8c0568c915035bef849581b
* https://github.com/vim/vim/commit/e392eb41f8dfc01bd13634e534ac6b4d505326f4
* https://github.com/vim/vim/commit/d042dc825c9b97dacd84d4728f88300da4d5b6b9
* https://github.com/vim/vim/commit/2c5e8e80eacf491d4f266983f534a77776c7ae83
* https://github.com/vim/vim/commit/256972a9849b5d575b62a6a71be5b6934b5b0e8b
* https://github.com/vim/vim/commit/cc7ff3fcd8c8fd7da6faac98a138b830ec5c00d8

### Comments/Research on specific patches

* 7.4.797:
 * Modified function [`redraw_asap`](https://github.com/neovim/neovim/blob/6383ea6e8e14350432f1fc7da519b54d0ed67f8c/src/nvim/screen.c#L239) was removed in https://github.com/vim/vim/commit/e0e41b30c61922e099a067ac5c137e745699a1aa, together with its only caller [`check_termcode`](https://github.com/neovim/neovim/blob/6383ea6e8e14350432f1fc7da519b54d0ed67f8c/src/nvim/term.c#L2803).
 * Grepping for the following regexps did not yield any result in nvim/src and its subdirectories: `rows.*\*.*Columns` (lines modified often),  `ScreenLinesC\[r\]` (one of the sources of the bug), `msg_scrolled` followed by grepping for `NORMAL` (another line that was changed for the bug)
 * The out-of-bound access was on  the array `*screenlineC[MAX_MCO]` (see the [diff](https://github.com/vim/vim/commit/5f95f288a2d303be1571e818655fd90e399ee58e#diff-ceb2e2231c5d45523135ca0cfc492792R349)). I grepped for `MAX_MCO` an checked every array of that length for out-of-bounds access in its scope (I did not check for called functions, e.g. `utfc_ptr2char(p, u8cc)` where `u8cc` was of length `MAX_MCO`). I did not find any.
 * The code for drawing on the screen was moved to the TUI, which was newly written.
 * Therefore, I believe the code that was patched does not exist in nvim anymore and the patch should be marked NA. Should ask [@tarruda](https://github.com/tarruda) for confirmation, though.