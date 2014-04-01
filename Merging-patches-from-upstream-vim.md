Description
-----------

This wiki page aims to keep track of what patches from upstream vim have been merged since the fork. The fork happened at version 7.4.160. This is a direct offshoot of issue #438 ([link](https://github.com/neovim/neovim/issues/438)).

Everyone is welcome to add new relevant patches to the table at the bottom of this page. Some types of patches are **never** relevant, notably:

- **Compiler warning fixes**: neovim strives to have no warnings at all, for now only on gcc and clang though, so the warnings have already been fixed.
- **#ifdef tweaking**: an example, recently vim decided to enable `FEAT_VISUAL` for all platforms and watch the fallout. Neovim has usually already done that.
- ... (add more)

Anything else might be relevant, it is preferable to err on the side of caution and when you don't know, please post in the issue to let others take a look. 

Pull requests
-------------

Merging in patches from upstream is a good way to get started with contributing to neovim, so don't hesitate to send your pull requests! Do note that the commit message needs to contain a token like `vim-patch:7.4.123` as suggested by @justinmk.

Table of patches
----------------

Version  | Description | Merged
------------------- | --------------- | ----------
 [7.4.164](https://code.google.com/p/vim/source/detail?r=a01819fb6e2b5c270dac492ab2fe923ea9301651)  | Problem with event handling on Windows 8. | ✗
 [7.4.166](https://code.google.com/p/vim/source/detail?r=5d03c374712128077ac4c342aad02120ed98df70)  | Auto-loading a function for code that won't be executed. | ✗
 [7.4.167](https://code.google.com/p/vim/source/detail?r=22387c8eec43ea8b1b704cad49c8f7187e2fd579)  | Fixes are not tested. Add a test for not autoloading on assignment. | ✗
 [7.4.169](https://code.google.com/p/vim/source/detail?r=4e3a9dd25d428e7c08ed401afc244972e27e08e6)  | ":sleep" puts cursor in the wrong column. | ✗
 [7.4.170](https://code.google.com/p/vim/source/detail?r=8122eab8fcdbbdaac62dfbf7c6458cb3e6f46b04)  | Some help tags don't work with ":help". | ✗
 [7.4.171](https://code.google.com/p/vim/source/detail?r=beb037a6c2708f539d50840637f70eed0811d93c)  | Redo does not set v:count and v:count1. | ✗
 [7.4.172](https://code.google.com/p/vim/source/detail?r=391e10afccf6879dcfab8b28cb1587a13eb835c0)  | The blowfish code mentions output feedback, but the code is actually doing cipher feedback. | ✗
 [7.4.173](https://code.google.com/p/vim/source/detail?r=233ad7b960d0fbeb224b383918113b25c74ebe35)  | When using scrollbind the cursor can end up below the last line.. | ✗
 [7.4.175](https://code.google.com/p/vim/source/detail?r=6b69d8dde19e32909f4ee3a6337e6a2ecfbb6f72)  | When a wide library function fails, falling back to the non-wide function may do the wrong thing. | ✗
 [runtime](https://code.google.com/p/vim/source/detail?r=1dea14d4c73897e0317779a1c85271629806def5)  | Update runtime files.  Add support for systemverilog. | ✗
 [7.4.178](https://code.google.com/p/vim/source/detail?r=647e6bb15aa3f864eaf447fe77e3e3ae7e37b134)  | The J command does not update '[ and '] marks. | ✗
 [7.4.181](https://code.google.com/p/vim/source/detail?r=cb5683bcde03796baa7e845fd9a2fcaec3383538)  | When using 'pastetoggle' the status lines are not updated. | ✗
 [7.4.183](https://code.google.com/p/vim/source/detail?r=1e2bfe4f3e903110f27cb6231f6642e721808837)  | MSVC Visual Studio update not supported. | ✗
 [7.4.184](https://code.google.com/p/vim/source/detail?r=9ac2fc63501d3eff92446c03b2822b30b169db5a)  | match() does not work properly with a {count} argument. | ✗
 [7.4.186](https://code.google.com/p/vim/source/detail?r=4d12112c5efae071aecbeed1a7196f18950457b3)  | Insert in Visual mode sometimes gives incorrect results. | ✗
 [7.4.187](https://code.google.com/p/vim/source/detail?r=a1c07956171a133583df42627d3498f935e59988)  | Delete that crosses line break splits multi-byte character. | ✗
 [7.4.191](https://code.google.com/p/vim/source/detail?r=40f18a1c1592c8b4047f6f2a413557f48a99c55f)  | Escaping a file name for shell commands can't be done without a function. | ✗
 [7.4.192](https://code.google.com/p/vim/source/detail?r=04c4ef8c0a1b757494500e46400552b135135e94)  | Memory leak when giving E853. | ✗
 [7.4.193](https://code.google.com/p/vim/source/detail?r=a8650e2a0b5a5936f7d503429180df47df2aa775)  | Typos in messages. | ✗
 [7.4.199](https://code.google.com/p/vim/source/detail?r=54b1a90c937380195fad6a52408aa3b4eed6d8d1)  | P doesn't paste over Visual selection. | ✗
 [7.4.201](https://code.google.com/p/vim/source/detail?r=06e5f65c34d8136c3a9d2219429b7eca35cb3a21)  | 'lispwords' is a global option. | ✗
 [7.4.202](https://code.google.com/p/vim/source/detail?r=22d7af9ff3e5e2b93fdbe8603df2f15155a5976b)  | MS-Windows: non-ASCII font names don't work. | ✗
 [7.4.203](https://code.google.com/p/vim/source/detail?r=fb24b025c7cf07db79a559a3091db42e02c1af86)  | Parsing 'errorformat' is not correct. | ✗
 [7.4.204](https://code.google.com/p/vim/source/detail?r=f5120cbf16b9a9c6e0fbb599a6524e05ecf11393)  | A mapping where the second byte is 0x80 doesn't work. | ✗
 [7.4.205](https://code.google.com/p/vim/source/list?r=f99b6efb51938d3d554be40a6d2d262e6cc5fff3)  | ":mksession" writes command to move to second argument while it does not exist.  When it does exist the order might be wrong. | ✗
 [7.4.207](https://code.google.com/p/vim/source/detail?r=2aa909427e44cd3aac7def024b66e41d0c9d0e0d)  | The cursor report sequence is sometimes not recognized and results in entering replace mode.  | ✗
 [7.4.209](https://code.google.com/p/vim/source/detail?r=bb402c49379de97fcd475fbbbbdc5ed41e5dff07)  | When repeating a filter command "%" and "#" are expanded. | ✗
 [7.4.210](https://code.google.com/p/vim/source/detail?r=420fd9cb86d51a92c4307a746557e81914c6d6c4)  | Visual block mode plus virtual edit doesn't work well with tabs. | ✗
 [7.4.211](https://code.google.com/p/vim/source/detail?r=e90bef2240c8d187da6e8d8fa5007ec5afc12284)  | ":lu" is an abbreviation for ":lua", but it should be ":lunmap". | ✗
 [7.4.213](https://code.google.com/p/vim/source/detail?r=e25a04c1c515e6eb32197291472f89bcadfabf89)  | It's not possible to open a new buffer without creating a swap file. | ✗
 [7.4.215](https://code.google.com/p/vim/source/detail?r=f069a3a0f84451aa498c6c22d8f922d1e695e96d)  | Inconsistency: ":sp foo" does not reload "foo", unless "foo" is the current buffer. | ✗
[7.4.218](https://code.google.com/p/vim/source/detail?r=ddc3f32a4b2191f829206322d46f0e9c7e365e22)  | It's not easy to remove duplicates from a list. **Add the uniq() function.** | ✗
 [7.4.219](https://code.google.com/p/vim/source/detail?r=37af1e6e91bb1e8ceb89d3ba1c49a04ffd889880)  | When 'relativenumber' or 'cursorline' are set the window is redrawn much to often. | ✗
[7.4.221](https://code.google.com/p/vim/source/detail?r=a548aae15b3a27a56d814900049785c29c01a37a)  | Quickfix doesn't resize on ":copen 20". | ✗
[7.4.226](https://code.google.com/p/vim/source/detail?r=b650f2db8f9604124c0ddfb14af0c04bd4ae0580)  | Cursurline highlighting not redrawn when scrolling. | ✗
[7.4.229](https://code.google.com/p/vim/source/detail?r=839cca5ec18d560e3714065e54ed38b6e812aaf7)  | Using ":let" for listing variables and the second one is a curly braces expression may fail. | ✗