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
    

Table of Patches
----------------

✔ Done &nbsp; ✗ To do &nbsp; `N/A` Won't patch &nbsp; `RFC` Request for comments

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
[7.4.241](https://code.google.com/p/vim/source/detail?r=a63d0cd691dc925283815d17d62f4e948d723a59)  | The string returned by submatch() does not distinguish between a NL from a line break and a NL that stands for a NUL character. ([#611](https://github.com/neovim/neovim/pull/611)) ([docs/#24](https://github.com/neovim/docs/pull/24))| ✔
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
[7.4.258](https://code.google.com/p/vim/source/detail?r=e8ffd1e6c8dc62c604d34e879791404bd15cab33)  | Configure fails if $CC contains options. | N/A
[7.4.259](https://code.google.com/p/vim/source/detail?r=e4cd5bb75029d2c1208f3e31ebde4e03b16e8123)  | Warning for misplaced "const". | **RFC**
[7.4.260](https://code.google.com/p/vim/source/detail?r=6bc874e4789a0f912b4fd6b23afecf19d80b1605)  | It is possible to define a function with a colon in the name.  It is possible to define a function with a lower case character if a "#" appears after the name. ([#602](https://github.com/neovim/neovim/pull/602))| ✔
[7.4.261](https://code.google.com/p/vim/source/detail?r=43c6cd07c8defd8505acbe479c6970764c08e6f9)  | When updating the window involves a regexp pattern, an interactive substitute to replace a "\n" with a line break fails. (Ingo Karkat) ([#600](https://github.com/neovim/neovim/pull/600))| ✔
[7.4.262](https://code.google.com/p/vim/source/detail?r=0ea551fa607dc443b97c2fba97dc0c9cb0bcf303)  | Duplicate code in regexec(). ([#630](https://github.com/neovim/neovim/pull/630)) | ✔
[7.4.263](https://code.google.com/p/vim/source/detail?r=af1bb39774f41c28eabd24d80cffc775695bc124)  | GCC 4.8 compiler warning for hiding a declaration (Francois Gannaz) | N/A
[7.4.264](https://code.google.com/p/vim/source/detail?r=00acac0af680c2d8c82db5258474b121a5908926)  | Can't define a function starting with "g:".  Can't assign a funcref to a buffer-local variable. ([#621](https://github.com/neovim/neovim/pull/621)) | ✔
[7.4.265](https://code.google.com/p/vim/source/detail?r=8ec9d2196bee0c5108f2d2c196a660a7f4e5f29f)  | Can't call a global function with "g:" in an expression. ([#641](https://github.com/neovim/neovim/pull/641))| ✔
[7.4.266](https://code.google.com/p/vim/source/detail?r=8f84e906d454a95d3167678a745dde9de442b604)  |Test 62 fails. ([#647](https://github.com/neovim/neovim/pull/647))| ✔
[7.4.267](https://code.google.com/p/vim/source/detail?r=75f222d67cea335efbe0274de6340dba174c1e7e)  |The '[ mark is in the wrong position after "gq". (Ingo Karkat) ([#756](https://github.com/neovim/neovim/pull/756))| ✔
[7.4.268](https://code.google.com/p/vim/source/detail?r=1a5ed2626b26a982e307a206572121a557adf709)  |Using exists() on a funcref for a script-local function does not work. ([#651](https://github.com/neovim/neovim/pull/651))  | ✔
[7.4.269](https://code.google.com/p/vim/source/detail?r=81c26975e8f9dc7435353581346542409403f296)  |CTRL-U in Insert mode does not work after using a cursor key. (Pine Wu) ([#648](https://github.com/neovim/neovim/pull/648))| ✔
[7.4.270](https://code.google.com/p/vim/source/detail?r=c519c446c5488bfd48c93a03efae4ae3e0c1f162) | Comparing pointers instead of the string they point to. | N/A
[7.4.271](https://code.google.com/p/vim/source/detail?r=88b0571de4327ba5127a483493bd7d46e6a9850e) | Compiler warning on 64 bit windows. | ✗
[7.4.272](https://code.google.com/p/vim/source/detail?r=00228400629e28384f7f52556c3c119ba0d0a44d) | Using just "$" does not cause an error message. ([#653](https://github.com/neovim/neovim/pull/653))| ✔
[runtime](https://code.google.com/p/vim/source/detail?r=306caa30d83b42d79685c472a4829a9aa43e72c8) | Runtime file updates. | ✗
[7.4.274](https://code.google.com/p/vim/source/detail?r=1ee3fc5b40ae94c2a7fc5a62bca38d4f730f9bb2) | When doing ":update" just before running an external command that changes the file, the timestamp may be unchanged and the file is not reloaded. ([#670](https://github.com/neovim/neovim/pull/670)) | ✔
[7.4.275](https://code.google.com/p/vim/source/detail?r=8a3117a4887c1e12a1165c9719491f96753787d6) | When changing the type of a sign that hasn't been placed ther is no error message. ([#738](https://github.com/neovim/neovim/pull/738))| ✔
[7.4.276](https://code.google.com/p/vim/source/detail?r=a6b59ee633a355095e6473ec5e2a7d9088bfb853) | The fish shell is not supported. ([#773](https://github.com/neovim/neovim/pull/773))| ✗
[7.4.277](https://code.google.com/p/vim/source/detail?r=373204662d82e894b27ee76bc3319bc62c91f6ae) | Using ":sign unplace *" may leave the cursor in the wrong position (Christian Brabandt) ([#744](https://github.com/neovim/neovim/pull/744))| ✔
[7.4.278](https://code.google.com/p/vim/source/detail?r=b4ce0e1fb5a67d7d6b0bca8eaa3edc2e94a085d8) | list_remove() conflicts with function defined in Sun header file. | ✗
[7.4.279](https://code.google.com/p/vim/source/detail?r=8e9db1f27a0063df023cc05a760fce73255dad24) | globpath() returns a string, making it difficult to get a list of matches. (Greg Novack) | ✗
[7.4.280](https://code.google.com/p/vim/source/detail?r=daf7e98675cf395e1ef96f8040567affb2782a11) | When using a session file the relative position of the cursor is not restored if there is another tab. (Nobuhiro Takasaki) ([#745](https://github.com/neovim/neovim/pull/745))| ✔
[7.4.281](https://code.google.com/p/vim/source/detail?r=24c90f1fec859b54cf2b854b98c4c9e614c46061) | When a session file has more than one tabpage and 'showtabline' is one the positions may be slightly off. ([#746](https://github.com/neovim/neovim/pull/746))| ✔
[7.4.282](https://code.google.com/p/vim/source/detail?r=6d0a1132dd71c7f55f7ed53fe99e97c79bfd05a4) | Test 97 fails on Mac. ([#747](https://github.com/neovim/neovim/pull/747))| ✔
[7.4.283](https://code.google.com/p/vim/source/detail?r=aa99d04fa7e288a8580e3a5d4a9d6433a1572b48) | Compiler warning about unused variable. (Charles Cooper) | ✗
[7.4.284](https://code.google.com/p/vim/source/detail?r=3c35ca9666e88a8024af6dab585b8e79ab295f83) | Setting 'langmap' in the modeline can cause trouble.  E.g. mapping	    ":" breaks many commands. (Jens-Wolfhard Schicke-Uffmann) ([#748](https://github.com/neovim/neovim/pull/748))| ✔
[7.4.285](https://code.google.com/p/vim/source/detail?r=5cb1828fd0056de3c166e71fbafc67a74c57d7b1) | When 'relativenumber' is set and deleting lines or undoing that,	    line numbers are not always updated. (Robert Arkwright) ([#749](https://github.com/neovim/neovim/pull/749))| ✔
[7.4.286](https://code.google.com/p/vim/source/detail?r=be19015ef43cc17825929206790696c2e716035d) | Error messages are inconsistant. (ZyX) ([#750](https://github.com/neovim/neovim/pull/750)) | ✔
[7.4.287](https://code.google.com/p/vim/source/detail?r=66fe4908b649ba18426af6f69e8ccb01b487dcbd) | Patches for .hgignore don't work, since the file is not in the	    distribution. | N/A
[7.4.288](https://code.google.com/p/vim/source/detail?r=7965cb6a435ae1ea331c7c2f8740d3d4c3625f3b) | When 'spellfile' is set the screen is not redrawn. ([#751](https://github.com/neovim/neovim/pull/751))| ✔
[7.4.289](https://code.google.com/p/vim/source/detail?r=99374096a76b96d1128f5e6aa1fa92b4ba70fee9) | Pattern with repeated backreference does not match with new regexp	    engine. (Urtica Dioica) ([#752](https://github.com/neovim/neovim/pull/752))| ✔
[7.4.290](https://code.google.com/p/vim/source/detail?r=b871734bf54ea185dbd2cc759d86dbfbe21cde26) | A non-greedy match followed by a branch is too greedy. (Ingo	    Karkat) ([#753](https://github.com/neovim/neovim/pull/753))| ✔
[7.4.291](https://code.google.com/p/vim/source/detail?r=b5972833add9de714f4651e26fd9ea63ec4a880c) | Compiler warning for int to pointer of different size when DEBUG	    is defined. ([#879](https://github.com/neovim/neovim/pull/879))| ✔
[7.4.292](https://code.google.com/p/vim/source/detail?r=60cdaa05a6ad31cef55eb6b3dc1f57ecac6fcf79) | Searching for "a" does not match accented "a" with new regexp	    engine, does match with old engine. (David Bürgin)	    "ca" does not match "ca" with accented "a" with either engine. ([#754](https://github.com/neovim/neovim/pull/754))| ✔
[7.4.293](https://code.google.com/p/vim/source/detail?r=10fc95f48546f438648b8357062e93c9c2c0a377) | It is not possible to ignore composing characters at a specific	    point in a pattern. ([#972](https://github.com/neovim/neovim/pull/972)) | ✗
[7.4.294](https://code.google.com/p/vim/source/detail?r=fdea5ea9afd139ea59dee6bdb3f1675b8b882bdf) | Test files missing from patch. ([#972](https://github.com/neovim/neovim/pull/972)) | ✗
[7.4.295](https://code.google.com/p/vim/source/detail?r=662ae48e7e246a63d38c9f3165b15b62252edaee) | Various typos, bad white space and unclear comments. ([#833](https://github.com/neovim/neovim/pull/833))| ✔
[7.4.296](https://code.google.com/p/vim/source/detail?r=53b87d790574b6d19034fb3390987c22fb928c58) | Can't run tests on Solaris. | N/A
[7.4.297](https://code.google.com/p/vim/source/detail?r=81f5a056b2a582c8109da10cc538dc16a326a34d) | Memory leak from result of get_isolated_shell_name(). | ✗
[7.4.298](https://code.google.com/p/vim/source/detail?r=156f891d520e93eab5d3ce02784660fb13a3b0d3) | Can't have a funcref start with "t:". ([#815](https://github.com/neovim/neovim/pull/815))| ✔
[7.4.299](https://code.google.com/p/vim/source/detail?r=daebf8ce66089c0c179fb436ceba359ef8d593d5) | When running configure twice DYNAMIC_PYTHON_DLL may become empty. | N/A
[7.4.300](https://code.google.com/p/vim/source/detail?r=1157079ca5f167bcf8746dfc52ea5a85e6c87a30) | The way config.cache is removed doesn't always work. | N/A
[7.4.301](https://code.google.com/p/vim/source/detail?r=8cb42aa3c4957a543e5dffe307475dbab969612f) | Still a scrolling problem when loading a session file. ([#816](https://github.com/neovim/neovim/pull/816))| ✔
[7.4.302](https://code.google.com/p/vim/source/detail?r=df141c80ea3a1ffcbf82d05c1314675231fcfa75) | Signs placed with 'foldcolumn' set don't show up after filler	    lines. ([#817](https://github.com/neovim/neovim/pull/817)) | ✔
[7.4.303](https://code.google.com/p/vim/source/detail?r=463ef551e9f62b63ac3f85f1f297b668b14bcd09) | When using double-width characters the text displayed on the	    command line is sometimes truncated. ([#818](https://github.com/neovim/neovim/pull/818))| ✔
[7.4.304](https://code.google.com/p/vim/source/detail?r=fed2e0967f8133ba9a44b0701f151c8d88c4896a) | Cannot always use Python with Vim. | N/A
[7.4.305](https://code.google.com/p/vim/source/detail?r=63e7cc62402dffb180b40c04c63ceeb5f53957d7) | Making 'ttymouse' empty after the xterm version was requested	    causes problems. (Elijah Griffin) ([#835](https://github.com/neovim/neovim/pull/835)) | ✗
[7.4.306](https://code.google.com/p/vim/source/detail?r=05e1d8afcc5e375bf708ccc9810e2fd1a5a8a3cf) | getchar(0) does not return Esc.	    Matsumoto) ([#842](https://github.com/neovim/neovim/pull/842)) | ✔
[7.4.307](https://code.google.com/p/vim/source/detail?r=06c10522d321d98874546b2a4d3b0ae145386f2e) | Can't build without the +termresponse feature. | ✗
[7.4.308](https://code.google.com/p/vim/source/detail?r=e3d2b8d83bb30c428a051f50791e454fcbc080af) | When using ":diffsplit" on an empty file the cursor is displayed	    on the command line. ([#832](https://github.com/neovim/neovim/pull/832))| ✔
[7.4.309](https://code.google.com/p/vim/source/detail?r=88a6e9f33822d33b6c32db578750c6c178c63f50) | When increasing the size of the lower window, the upper window	    jumps back to the top. (Ron Aaron) ([#843](https://github.com/neovim/neovim/pull/843))| ✗
[7.4.310](https://code.google.com/p/vim/source/detail?r=ccac0aa34eeaf46dad4b831461a532fc3fe71096) | getpos()/setpos() don't include curswant. ([#919](https://github.com/neovim/neovim/pull/919)) | ✗
[7.4.311](https://code.google.com/p/vim/source/detail?r=f6f7543043246107075f0d3739c471d51b7226da) | Can't use winrestview to only restore part of the view. ([#906](https://github.com/neovim/neovim/pull/906))| ✗
[7.4.312](https://code.google.com/p/vim/source/detail?r=66eead134d6800fd4cf2d5d4b135d300c933f09a) | Cannot figure out what argument list is being used for a window. | ✗
[7.4.313](https://code.google.com/p/vim/source/detail?r=332a5c2b2956d9b18d85268a724d01deea27ec83) | Changing the return value of getpos() causes an error. (Jie Zhu) | ✗
[7.4.314](https://code.google.com/p/vim/source/detail?r=4d7af1962d6ce61df65fdc5c86544a61951f9517) | Completion messages can get in the way of a plugin. ([#971](https://github.com/neovim/neovim/pull/971)) | ✗
[7.4.315](https://code.google.com/p/vim/source/detail?r=646616b6ff4defcc7bef0b198b540f6d965a8126) | Fixes for computation of topline not tested. | ✗
[7.4.316](https://code.google.com/p/vim/source/detail?r=0fc665889e8f0af532cb4e3be2f0ff0421bf2fbc) | Warning from 64-bit compiler. | ✗
[7.4.317](https://code.google.com/p/vim/source/detail?r=8ffcb546d782121dfc9d88c7edc6f62421efce89) | Crash when starting gvim.  Issue 230. | ✗
[7.4.318](https://code.google.com/p/vim/source/detail?r=5c47dacf397c1c65d2dfc237b3ff395c66ec3d4d) | Check for whether a highlight group has settings ignores fg and bg color settings. ([#968](https://github.com/neovim/neovim/pull/968))| RFC
[7.4.319](https://code.google.com/p/vim/source/detail?r=a076237d1c3849535681e82946a9041ed5525d7f) | Crash when putting zero bytes on the clipboard. | ✗
[7.4.320](https://code.google.com/p/vim/source/detail?r=f7bc601823e5c81e2ca412506a42eff9fd790ace) | Possible crash when an BufLeave autocommand deletes the buffer. | ✗
[7.4.321](https://code.google.com/p/vim/source/detail?r=c052937aae8ca5082f308b8ff0712c7eccdd30c8) | Can't build with strawberry perl 5.20 + mingw-w64-4.9.0. | N/A
[7.4.322](https://code.google.com/p/vim/source/detail?r=fd96c55d683d76ece4ba01490d9796c13c988cdc) | Using "msgfmt" is hard coded, cannot use "gmsgfmt". | N/A
[7.4.323](https://code.google.com/p/vim/source/detail?r=238f5027830cad22e17a970483af9b160869cdf3) | Substitute() with zero width pattern breaks multi-byte character. ([#967](https://github.com/neovim/neovim/pull/967)) | RFC
[7.4.324](https://code.google.com/p/vim/source/detail?r=c476e0ac8b406693c3877baffa0e97ff25e59b06) | In Ex mode, cyrillic characters are not handled. (Stas Malavin) | ✗
[7.4.325](https://code.google.com/p/vim/source/detail?r=1f288d2475488c3f44c7248e99019e2612580716) | When starting the gui and changing the window size the status line	    may not be drawn correctly. | N/A
[7.4.326](https://code.google.com/p/vim/source/detail?r=1dbcb23ae7a8b68ddbc28b4feb794c4c1db12395) | Can't build Tiny version. (Elimar Riesebieter) | N/A
[7.4.327](https://code.google.com/p/vim/source/detail?r=99d8f2d72dcd4b850de81998cc9b1120c8165762) | When 'verbose' is set to display the return value of a function,	    may get E724 repeatedly. | ✗
[7.4.328](https://code.google.com/p/vim/source/detail?r=01d9ffdd6e6ffb39faf946e13ec63bd7dc31e162) | Selection of inner block is inconsistent. ([#970](https://github.com/neovim/neovim/pull/970))| RFC
[7.4.329](https://code.google.com/p/vim/source/detail?r=018df65085f8990c1407442f8c783d4cee72a479) | When moving the cursor and then switching to another window the	    previous window isn't scrolled. (Yukihiro Nakadaira) | ✗
[7.4.330](https://code.google.com/p/vim/source/detail?r=f9fa2e506b9f07549cd91074835c5c553db7b3a7) | Using a regexp pattern to highlight a specific position can be	    slow. | ✗
[7.4.331](https://code.google.com/p/vim/source/detail?r=6d984caa0409fd284722c44cb09a0a2b5360bd4f) | Relative numbering not updated after a linewise yank.  Issue 235. | ✗
[7.4.332](https://code.google.com/p/vim/source/detail?r=8fed02d53b45848b0fff60de13d06858963cfb17) | GTK: When a sign icon doesn't fit exactly there can be ugly gaps. | N/A
[7.4.333](https://code.google.com/p/vim/source/detail?r=8ae50e3ef8bf733c0869c01b5132d02feffc0955) | Compiler warning for unused function. | ✗
[7.4.334](https://code.google.com/p/vim/source/detail?r=03d260a8ea0c0c67f424c387dbe2af5754e5e589) | Unitialized variables, causing some problems. | ✗
[7.4.335](https://code.google.com/p/vim/source/detail?r=8ad2ecd116021ad5c945426e8bb80d741392b780) | No digraph for the new rouble sign. | ✗
[7.4.336](https://code.google.com/p/vim/source/detail?r=a42ba1e5099290a86cac1a9ac490c49e82e4c2cf) | Setting 'history' to a big value causes out-of-memory errors. ([#991](https://github.com/neovim/neovim/pull/991)) | RFC
[7.4.337](https://code.google.com/p/vim/source/detail?r=0206ac84ff5fdce6d893c470e0909d2aed547a24) | When there is an error preparing to edit the command line, the command won't be executed. (Hirohito Higashi) | ✗
[7.4.338](https://code.google.com/p/vim/source/detail?r=ef83b423ebf7de11c1063c795dd2186a9b59b90f) | Cannot wrap lines taking indent into account. | RFC
[7.4.339](https://code.google.com/p/vim/source/detail?r=fd7110d0c3bf4fea3cfa3d16da6c2a945d327c27) | Local function is available globally. | ✗
[7.4.340](https://code.google.com/p/vim/source/detail?r=03f95f5e311b84653df70fb3c08a9d92cf21b8f0) | Error from sed about illegal bytes when installing Vim. | N/A
[7.4.341](https://code.google.com/p/vim/source/detail?r=adc4a84f72eb44dae657af713922a6e2c1f64ae3) | sort() doesn't handle numbers well. | ✗
[7.4.342](https://code.google.com/p/vim/source/detail?r=8dcc6f142460b2d5eee119a174d441d46d95cd99) | Clang gives warnings. | N/A
[7.4.343](https://code.google.com/p/vim/source/detail?r=539ce56d8f35fe2deb5c4f57335e1adf97ae4e74) | matchdelete() does not always update the right lines. | ✗
[7.4.344](https://code.google.com/p/vim/source/detail?r=ce284c205558d103326a4c3f22f181774690b3eb) | Unessecary initializations and other things related to matchaddpos(). | ✗
[7.4.345](https://code.google.com/p/vim/source/detail?r=ea2c5dfee1b04d216ebf992c5f46ecbdfee2854a) | Indent is not updated when deleting indent. | ✗
[7.4.346](https://code.google.com/p/vim/source/detail?r=3248c6e40aee01a7254d111dd846c6ec7889a804) | Indent is not updated when changing 'breakindentopt'. (itchyny) | ✗
[7.4.347](https://code.google.com/p/vim/source/detail?r=a162d41f10e1c3c8673d86d8b0c58fdaf1bddeaf) | test55 fails on some systems. | ✗
[7.4.348](https://code.google.com/p/vim/source/detail?r=0b7586868f6da0372af7510650240e22dc1e6e64) | When using "J1" in 'cinoptions' a line below a continuation line gets too much indent. | ✗
[7.4.349](https://code.google.com/p/vim/source/detail?r=79950dae1d7de8fc2cb0f8ddd087d403e2b9ce8e) | When there are matches to highlight the whole window is redrawn, which is slow. | ✗
[7.4.350](https://code.google.com/p/vim/source/detail?r=ad005d0114c1d2d83490787ef7ea2a3c6e5e7b9e) | Using C indenting for Javascript does not work well for a {} block inside parenthesis. | ✗
[7.4.351](https://code.google.com/p/vim/source/detail?r=f9ec944e4474c649faad642797ffd798a7102549) | sort() is not stable. | ✗
[7.4.352](https://code.google.com/p/vim/source/detail?r=b4962cf3a1c06a1f60f1d750df8fcf7035b00b99) | With 'linebreak' a tab causes a missing line break. | ✗
[7.4.353](https://code.google.com/p/vim/source/detail?r=d42a1d3b74d40f580359dbd139d2d0dfa7235252) | 'breakindent' doesn't work with the 'list' option. | ✗
[7.4.354](https://code.google.com/p/vim/source/detail?r=5deaa4e9812d4b4ae59d8a3e70bf19983e07e6da) | Compiler warning. | ✗
[7.4.355](https://code.google.com/p/vim/source/detail?r=9a4efda75b5ef0f496d6a29c0a4dfcc7c03412f9) | Several problems with Javascript indenting. | ✗