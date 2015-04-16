In an online conversation, Istvan Albert was complaining he could not find a
good Smith-Waterman implementation in Javascript. I thought I could write one
over night by porting ksw.c to javascript. It took longer than I planned
because I found a couple of subtle bugs in ksw.c. And while I was porting the C
code to javascript, I realized that it is not that difficult to merge local and
banded global alignments in one function. Achieving that also took extra time.

The end product is a fast and lightweight javascript library for affine-gap
local and banded global pairwise alignment. With a modern Javascript engine, it
is not much slower than a non-SSE C implementation.

The inline comments briefly explain the APIs. Here is a tiny example:
```html
<script language="JavaScript" src="bioseq.js"></script>
<script type="text/javascript">
var target = 'ATAGCTAGCTAGCATAAGC';
var query  = 'AGCTAcCGCAT';
var isLocal = false;
var match = 1, mis = -1, gapOpen = -1, gapExt = -1
var rst = bsa_align(isLocal, target, query, [match,mis], [gapOpen,gapExt]);
var str = 'score='+rst[0]+'; pos='+rst[1]+'; cigar='+bsa_cigar2str(rst[2])+"\n";
var fmt = bsa_cigar2gaps(target, query, rst[1], rst[2]);
str += fmt[0] + '\n' + fmt[1] + '\n';
alert(str);
</script>
```
More complete interface is the HTML page in this repo. A live demo is
[here][demo].



[demo]: http://lh3lh3.users.sourceforge.net/bioseq.shtml
