Description
-----------

This wiki page aims to keep track of what patches from upstream vim have been merged since the fork. The fork happened at version 7.4.160. This is a direct offshoot of [issue #438](https://github.com/neovim/neovim/issues/438).

Everyone is welcome to add new relevant patches to the table at the [bottom of this page](#table-of-patches). Some types of patches are **never** relevant, notably:

- **Compiler warning fixes**: neovim strives to have no warnings at all, for now only on gcc and clang though, so the warnings have already been fixed.
- **#ifdef tweaking**: an example, recently vim decided to enable `FEAT_VISUAL` for all platforms and watch the fallout. Neovim has usually already done that.
- **Legacy system support**: Fixes for legacy systems such as Solaris, Amiga, Xenix are not needed since they are not supported by neovim.
- (add more...)

Anything else might be relevant, it is preferable to err on the side of caution and when you don't know, please post in the issue to let others take a look. 

Pull requests
-------------

Merging in patches from upstream is a good way to get started with contributing to neovim, so don't hesitate to send your pull requests! 

Commit message should include:

- a token indicating the Vim patch number, formatted as follows (no space!): `vim-patch:7.4.123`
- a URL pointing to the Vim online repository commit:
    - https://code.google.com/p/vim/source/detail?r=5d03c374712128077ac4c342aad02120ed98df70
- the original Vim patch commit message, including the author
    

Table of patches
----------------

## Legend ##

✔ Done
✗ To do (or won't patch ?)
N/A Won't patch
RFC Request for comments

Version  | Description | Merged
------------------- | --------------- | ----------
 [7.4.164](https://code.google.com/p/vim/source/detail?r=a01819fb6e2b5c270dac492ab2fe923ea9301651)  | Problem with event handling on Windows 8. | N/A
 [7.4.166](https://code.google.com/p/vim/source/detail?r=5d03c374712128077ac4c342aad02120ed98df70)  | Auto-loading a function for code that won't be executed. ([#445](https://github.com/neovim/neovim/pull/445)) | ✔
 [7.4.167](https://code.google.com/p/vim/source/detail?r=22387c8eec43ea8b1b704cad49c8f7187e2fd579)  | Fixes are not tested. Add a test for not autoloading on assignment. ([#499](https://github.com/neovim/neovim/pull/499))| ✔
 [7.4.169](https://code.google.com/p/vim/source/detail?r=4e3a9dd25d428e7c08ed401afc244972e27e08e6)  | ":sleep" puts cursor in the wrong column. ([#453](https://github.com/neovim/neovim/pull/453)) | ✔
 [7.4.170](https://code.google.com/p/vim/source/detail?r=8122eab8fcdbbdaac62dfbf7c6458cb3e6f46b04)  | Some help tags don't work with ":help". ([#454](https://github.com/neovim/neovim/pull/454)) | ✔
 [7.4.171](https://code.google.com/p/vim/source/detail?r=beb037a6c2708f539d50840637f70eed0811d93c)  | Redo does not set v:count and v:count1. ([#455](https://github.com/neovim/neovim/pull/455)) | ✔
 [7.4.172](https://code.google.com/p/vim/source/detail?r=391e10afccf6879dcfab8b28cb1587a13eb835c0)  | The blowfish code mentions output feedback, but the code is actually doing cipher feedback. ([#456](https://github.com/neovim/neovim/pull/456)) | ✔
 [7.4.173](https://code.google.com/p/vim/source/detail?r=233ad7b960d0fbeb224b383918113b25c74ebe35)  | When using scrollbind the cursor can end up below the last line.. ([#457](https://github.com/neovim/neovim/pull/457)) | ✔
 [7.4.175](https://code.google.com/p/vim/source/detail?r=6b69d8dde19e32909f4ee3a6337e6a2ecfbb6f72)  | When a wide library function fails, falling back to the non-wide function may do the wrong thing. | N/A
 [runtime](https://code.google.com/p/vim/source/detail?r=1dea14d4c73897e0317779a1c85271629806def5)  | Update runtime files.  Add support for systemverilog. ([docs/#3](https://github.com/neovim/docs/pull/3)) ([vimscript/#3](https://github.com/neovim/vimscript/pull/3))| ✔
 [7.4.178](https://code.google.com/p/vim/source/detail?r=647e6bb15aa3f864eaf447fe77e3e3ae7e37b134)  | The J command does not update '[ and '] marks. ([#458](https://github.com/neovim/neovim/pull/458)) | ✔
 [7.4.181](https://code.google.com/p/vim/source/detail?r=cb5683bcde03796baa7e845fd9a2fcaec3383538)  | When using 'pastetoggle' the status lines are not updated. ([#468](https://github.com/neovim/neovim/pull/468)) | ✔
 [7.4.183](https://code.google.com/p/vim/source/detail?r=1e2bfe4f3e903110f27cb6231f6642e721808837)  | MSVC Visual Studio update not supported. | N/A
 [7.4.184](https://code.google.com/p/vim/source/detail?r=9ac2fc63501d3eff92446c03b2822b30b169db5a)  | match() does not work properly with a {count} argument. ([#469](https://github.com/neovim/neovim/pull/469)) | ✔
 [7.4.186](https://code.google.com/p/vim/source/detail?r=4d12112c5efae071aecbeed1a7196f18950457b3)  | Insert in Visual mode sometimes gives incorrect results. ([#479](https://github.com/neovim/neovim/pull/479)) | ✔
 [7.4.187](https://code.google.com/p/vim/source/detail?r=a1c07956171a133583df42627d3498f935e59988)  | Delete that crosses line break splits multi-byte character. ([#492](https://github.com/neovim/neovim/pull/492)) | ✔
 [7.4.191](https://code.google.com/p/vim/source/detail?r=40f18a1c1592c8b4047f6f2a413557f48a99c55f)  | Escaping a file name for shell commands can't be done without a function. ([#520](https://github.com/neovim/neovim/pull/520)) ([docs/#3](https://github.com/neovim/docs/pull/3))| ✔
 [7.4.192](https://code.google.com/p/vim/source/detail?r=04c4ef8c0a1b757494500e46400552b135135e94)  | Memory leak when giving E853. ([#494](https://github.com/neovim/neovim/pull/494))| ✔
 [7.4.193](https://code.google.com/p/vim/source/detail?r=a8650e2a0b5a5936f7d503429180df47df2aa775)  | Typos in messages. ([#495](https://github.com/neovim/neovim/pull/495))| ✔
 [7.4.199](https://code.google.com/p/vim/source/detail?r=54b1a90c937380195fad6a52408aa3b4eed6d8d1)  | P doesn't paste over Visual selection. ([#484](https://github.com/neovim/neovim/pull/484))| ✔
 [7.4.201](https://code.google.com/p/vim/source/detail?r=06e5f65c34d8136c3a9d2219429b7eca35cb3a21)  | 'lispwords' is a global option. | ✗
 [7.4.202](https://code.google.com/p/vim/source/detail?r=22d7af9ff3e5e2b93fdbe8603df2f15155a5976b)  | MS-Windows: non-ASCII font names don't work. | N/A
 [7.4.203](https://code.google.com/p/vim/source/detail?r=fb24b025c7cf07db79a559a3091db42e02c1af86)  | Parsing 'errorformat' is not correct. ([#505](https://github.com/neovim/neovim/pull/505))  | ✔
 [7.4.204](https://code.google.com/p/vim/source/detail?r=f5120cbf16b9a9c6e0fbb599a6524e05ecf11393)  | A mapping where the second byte is 0x80 doesn't work. ([#506](https://github.com/neovim/neovim/pull/506))  | ✔
 [7.4.205](https://code.google.com/p/vim/source/detail?r=0ace3a24c2a0153f0aaf9b619d3958e7f486705f)  | ":mksession" writes command to move to second argument while it does not exist. When it does exist the order might be wrong. ([#508](https://github.com/neovim/neovim/pull/508)) | ✔
 [7.4.207](https://code.google.com/p/vim/source/detail?r=2aa909427e44cd3aac7def024b66e41d0c9d0e0d)  | The cursor report sequence is sometimes not recognized and results in entering replace mode. ([#514](https://github.com/neovim/neovim/pull/514)) | ✔
 [7.4.209](https://code.google.com/p/vim/source/detail?r=bb402c49379de97fcd475fbbbbdc5ed41e5dff07)  | When repeating a filter command "%" and "#" are expanded. ([#515](https://github.com/neovim/neovim/pull/515))| ✔
 [7.4.210](https://code.google.com/p/vim/source/detail?r=420fd9cb86d51a92c4307a746557e81914c6d6c4)  | Visual block mode plus virtual edit doesn't work well with tabs. ([#516](https://github.com/neovim/neovim/pull/516))| ✔
 [7.4.211](https://code.google.com/p/vim/source/detail?r=e90bef2240c8d187da6e8d8fa5007ec5afc12284)  | ":lu" is an abbreviation for ":lua", but it should be ":lunmap". ([#521](https://github.com/neovim/neovim/pull/521))| ✗
 [7.4.213](https://code.google.com/p/vim/source/detail?r=e25a04c1c515e6eb32197291472f89bcadfabf89)  | It's not possible to open a new buffer without creating a swap file. ([#522](https://github.com/neovim/neovim/pull/522)) ([docs/#14](https://github.com/neovim/docs/pull/14))| ✔
 [7.4.215](https://code.google.com/p/vim/source/detail?r=f069a3a0f84451aa498c6c22d8f922d1e695e96d)  | Inconsistency: ":sp foo" does not reload "foo", unless "foo" is the current buffer. ([#524](https://github.com/neovim/neovim/pull/524)) ([docs/#15](https://github.com/neovim/docs/pull/15))| ✔
[7.4.218](https://code.google.com/p/vim/source/detail?r=ddc3f32a4b2191f829206322d46f0e9c7e365e22)  | It's not easy to remove duplicates from a list. **Add the uniq() function.** ([#525](https://github.com/neovim/neovim/pull/525))| ✔
 [7.4.219](https://code.google.com/p/vim/source/detail?r=37af1e6e91bb1e8ceb89d3ba1c49a04ffd889880)  | When 'relativenumber' or 'cursorline' are set the window is redrawn much to often. ([#517](https://github.com/neovim/neovim/pull/517))| ✔
[7.4.221](https://code.google.com/p/vim/source/detail?r=a548aae15b3a27a56d814900049785c29c01a37a)  | Quickfix doesn't resize on ":copen 20". ([#527](https://github.com/neovim/neovim/pull/527))| ✔
[7.4.226](https://code.google.com/p/vim/source/detail?r=b650f2db8f9604124c0ddfb14af0c04bd4ae0580)  | Cursurline highlighting not redrawn when scrolling. ([#554](https://github.com/neovim/neovim/pull/554)) | ✔
[7.4.229](https://code.google.com/p/vim/source/detail?r=839cca5ec18d560e3714065e54ed38b6e812aaf7)  | Using ":let" for listing variables and the second one is a curly braces expression may fail. ([#528](https://github.com/neovim/neovim/pull/528)) | ✔
[7.4.230](https://code.google.com/p/vim/source/detail?r=57ecd7a8c0f052296b41b916eb1ae7f2a9a48b27)  | Error when using ":options". | ✗
[7.4.231](https://code.google.com/p/vim/source/detail?r=0a295a3c9e473512ad3b006a0fb752ad43d19094)  | An error in ":options" is not caught by the tests. | ✗
[7.4.232](https://code.google.com/p/vim/source/detail?r=845608965bd9d0b2755997a7be812746885ff105)  | ":%s/\n//" uses a lot of memory. ([#529](https://github.com/neovim/neovim/pull/529)) | ✔
[7.4.233](https://code.google.com/p/vim/source/detail?r=22a1d5762ba3a75984e89dcc47a65498f63a6c2c)  | Escaping special characters for using "%" with a shell command is inconsistent, parenthesis are escaped but spaces are not. ([#530](https://github.com/neovim/neovim/pull/530)) | ✔
[7.4.234](https://code.google.com/p/vim/source/detail?r=d2286df8719d6e99c743e3bf6ac14d1f9debc84d)  | Add v:progpath. ([#531](https://github.com/neovim/neovim/pull/531)) | ✔
[7.4.235](https://code.google.com/p/vim/source/detail?r=5ab2946f7ce560985830fbc3c453bb0f7a01f385)  | Add the exepath() function. | ✗
[7.4.236](https://code.google.com/p/vim/source/detail?r=a44087db72386d080e9da870d751daf498004be8)  | Make has("patch-7.4.123") work. ([#561](https://github.com/neovim/neovim/pull/561)) | ✔
[7.4.237](https://code.google.com/p/vim/source/detail?r=71b165a378ad580818f6d497ecf0f8ad054a9683)  | When some patches was not included has("patch-7.4.123") may return true falsely. ([#569](https://github.com/neovim/neovim/pull/569)) ([docs/#21](https://github.com/neovim/docs/pull/21))| ✔
[7.4.238](https://code.google.com/p/vim/source/detail?r=410ef4f1a3d2f4a6ecad9aaa87dae645d1578a19)  | Add smack support | **RFC**
[7.4.239](https://code.google.com/p/vim/source/detail?r=98bfec9ea7608f312129475d4ca0ae6d1c6c232e)  | ":e +" does not position cursor at end of the file. ([#532](https://github.com/neovim/neovim/pull/532)) | ✔
[7.4.240](https://code.google.com/p/vim/source/detail?r=8d1ba0a23588932d22ad37cbd87ae3bbd4bfeff8)  | ":tjump" shows "\n" as "\\n". ([#533](https://github.com/neovim/neovim/pull/533)) | ✔
[7.4.241](https://code.google.com/p/vim/source/detail?r=a63d0cd691dc925283815d17d62f4e948d723a59)  | The string returned by submatch() does not distinguish between a NL from a line break and a NL that stands for a NUL character. ([#611](https://github.com/neovim/neovim/pull/611))| ✗
[7.4.242](https://code.google.com/p/vim/source/detail?r=f084024c0ddbba46aabfafa2996c3f7d13080ab6)  | getreg() does not distinguish between a NL used for a line break and a NL used for a NUL character. | ✗
[7.4.243](https://code.google.com/p/vim/source/detail?r=9f8fa56f1906f4f634cd602a7a2b4f8631faf526)  | Cannot use setreg() to add text that includes a NUL. | ✗
[7.4.244](https://code.google.com/p/vim/source/detail?r=da17c7de616e3829e4f59923ffa138a067928d9e)  | The smack feature causes stray error messages. | **RFC**
[7.4.245](https://code.google.com/p/vim/source/detail?r=80421d934ebde183ce545ab8d9eb3a4c2065c169)  | Crash for "vim -u NONE -N  -c '&&'". ([#555](https://github.com/neovim/neovim/pull/555)) | ✔
[7.4.247](https://code.google.com/p/vim/source/detail?r=9f8fa56f1906f4f634cd602a7a2b4f8631faf526)  | When passing input to system() there is no way to keep NUL and NL characters separate. | ✗
[7.4.248](https://code.google.com/p/vim/source/detail?r=e5f1f2ea0b4a4834791924880f78272ef52eb087)  | Cannot distinguish between NL and NUL in output of system(). | ✗
[7.4.249](https://code.google.com/p/vim/source/detail?r=0b9a66ea49f435536745be0e0a6154be7b607249)  | Using setreg() with a list of numbers does not work. | ✗
[7.4.250](https://code.google.com/p/vim/source/detail?r=a8f3f45896288bd7e0a27e0c28c3cc3457ccc507)  | Some test files missing from distribution. | **RFC**
[7.4.251](https://code.google.com/p/vim/source/detail?r=29eb4c2a33ac701bfcd4d2e2bed7864eba876e0e)  | Crash when BufAdd autocommand wipes out the buffer. ([#534](https://github.com/neovim/neovim/pull/534)) | ✔
[7.4.253](https://code.google.com/p/vim/source/detail?r=4901a36479f200b2e6700ad91c26911d92deb886)  | Crash when using cpp syntax file with pattern using external match. ([#535](https://github.com/neovim/neovim/pull/535)) | ✔
[7.4.254](https://code.google.com/p/vim/source/detail?r=251acc686ca41e4bccb037ef44cd7b486774d580)  | Smack support detection is incomplete. | **RFC**
[7.4.255](https://code.google.com/p/vim/source/detail?r=5595506b985a198abae41ab0150ee50b8bf1686c)  | Configure check for smack doesn't work with all shells. (David Larson) | **RFC**
[7.4.256](https://code.google.com/p/vim/source/detail?r=afb542ea210cb9fc5fa8c5359bb4814370024b80)  | Using systemlist() may cause a crash and does not handle NUL characters properly. | ✗
[7.4.257](https://code.google.com/p/vim/source/detail?r=17903ded5e9a9d49ca73b324657b944f2954d4fd)  | Compiler warning, possibly for mismatch in parameter name. | N/A
[7.4.258](https://code.google.com/p/vim/source/detail?r=e8ffd1e6c8dc62c604d34e879791404bd15cab33)  | Configure fails if $CC contains options. | ✗
[7.4.259](https://code.google.com/p/vim/source/detail?r=e4cd5bb75029d2c1208f3e31ebde4e03b16e8123)  | Warning for misplaced "const". | **RFC**
[7.4.260](https://code.google.com/p/vim/source/detail?r=6bc874e4789a0f912b4fd6b23afecf19d80b1605)  | It is possible to define a function with a colon in the name.  It is possible to define a function with a lower case character if a "#" appears after the name. ([#602](https://github.com/neovim/neovim/pull/602))| ✔
[7.4.261](https://code.google.com/p/vim/source/detail?r=43c6cd07c8defd8505acbe479c6970764c08e6f9)  | When updating the window involves a regexp pattern, an interactive substitute to replace a "\n" with a line break fails. (Ingo Karkat) ([#600](https://github.com/neovim/neovim/pull/600))| ✔
[7.4.262](https://code.google.com/p/vim/source/detail?r=0ea551fa607dc443b97c2fba97dc0c9cb0bcf303)  | Duplicate code in regexec(). ([#630](https://github.com/neovim/neovim/pull/630)) | ✗
[7.4.263](https://code.google.com/p/vim/source/detail?r=af1bb39774f41c28eabd24d80cffc775695bc124)  | GCC 4.8 compiler warning for hiding a declaration (Francois Gannaz) | ✗
[7.4.264](https://code.google.com/p/vim/source/detail?r=00acac0af680c2d8c82db5258474b121a5908926)  | Can't define a function starting with "g:".  Can't assign a funcref to a buffer-local variable. ([#621](https://github.com/neovim/neovim/pull/621)) | ✗
[7.4.265](https://code.google.com/p/vim/source/detail?r=8ec9d2196bee0c5108f2d2c196a660a7f4e5f29f)  | Can't call a global function with "g:" in an expression. | ✗