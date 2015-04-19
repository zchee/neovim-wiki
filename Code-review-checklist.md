Many items were [taken from here][code-review-checklist] [and here][code-review-secrets].

#### Code

- Is the Travis build passing?
- Does the code conform to the [style guide][style-guide]?
- Does the code work? Does it perform its intended function, the logic is
  correct, etc.
- Is the code easily understood?
- Is there any redundant or duplicate code?
- Are there any unused variables?
- Is the code as modular as possible?
- Can any global/static variables be replaced?
- Can any function attributes be used?
- Are variables/functions named intuitively?
- Can any of the code be replaced with library functions?
- Can any logging or debugging code be removed?
- Do loops have a set length and correct termination conditions?
- Are return values being checked?
- Are invalid parameter values handled where needed?
- Are there any use after frees?
- Are there any resource leaks? Memory leaks, unclosed sockets, etc.
- Are there any null pointer dereferences?
- Are any uninitialized variables used?
- Are there any cases of possible arithmetic overflow?
- Are there any unneeded assert statements?
- Is memory usage acceptable, even with large inputs?
- Optimization that makes code harder to read should only be implemented if a
  profiler or other tool has indicated that the routine stands to gain from
  optimization. These kinds of optimizations should be well-documented and
  code that performs the same task simply should be preserved somewhere.
- For new code, are unit tests written where needed?

#### Documentation

- Are there any superfluous comments?
- Where needed, do comments exist and describe the intent of the code?
- Are any comments made outdated by the new code?
- Is any unusual behavior or edge-case handling described?
- Are complex algorithms explained and justified?
- Is code that depends on non-obvious behavior in external libraries
  documented with reference to external documentation?
- Is the use and function of API functions documented?
- Are data structures/typedefs explained?
- Is there any incomplete code, e.g., code marked `TODO`, `FIXME`, or `XXX`?

[code-review-checklist]: http://blog.fogcreek.com/increase-defect-detection-with-our-code-review-checklist-example/
[code-review-secrets]: http://smartbear.com/SmartBear/media/pdfs/best-kept-secrets-of-peer-code-review.pdf
[style-guide]: http://neovim.io/develop/style-guide.xml
