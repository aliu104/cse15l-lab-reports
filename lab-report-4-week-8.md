# Week 8 - Lab Report 4
## ***DEBUGGING WITH `MARKDOWN-PARSE`***

#### In this lab, you will test whether your peer's and your `markdown-parse` code works for 3 new markdown snippets.
---
### **Links to Repositories**
- My `markdown-parse` repository: [Link](https://github.com/aliu104/markdown-parse)
- My peer's `markdown-parse` repository: [Link](https://github.com/annakkin/markdown-parse)

--
### **Snippet 1: Inline Code With Backticks**
*Expected Output*
![Image](labreport4-screenshots\labreport4-1.1.png)
```
["`google.com", "google.com", "ucsd.edu"]
```


*Creating a Test for this Snippet*
![Image](labreport4-screenshots\labreport4-1.2.png)


*My Implementation -- Failed*
![Image](labreport4-screenshots\labreport4-1.3a.png)
My implementation of `markdown-parse` failed for snippet 1. My code failed to recognize that backtick marks indicate a code segment. However, this could be easily fixed by adding an `if` statement in the beginning of the `while` loop in the `getLinks` method to disregard anything in between a pair of backticks. (If there is only a single backtick, we can proceed as usual.) 

*My Peer's Implementation -- Failed*
![Image](labreport4-screenshots\labreport4-1.3b.png)
My peer's implementation of `markdown-parse` failed for snippet 1. Similar to my implementation, their code did not recognize backticks and how they create inline code segments. The fix I mentioned in my implementation will also work for my peer's `getLinks` method. However, this failed test case also exposes another flaw in my peer's code: Links are only extracted after `](`, which may become problematic when we deal with nested parentheses/brackets.

--

### **Snippet 2: Nested Brackets, Parentheses, etc.**
*Expected Output*
![Image](labreport4-screenshots\labreport4-2.1.png)
```
["a.com", "a.com(())", "example.com"]
```


*Creating a Test for this Snippet*
![Image](labreport4-screenshots\labreport4-2.2.png)


*My Implementation -- Failed*
![Image](labreport4-screenshots\labreport4-2.3a.png)
My implementation of `markdown-parse` failed for snippet 2. While my code was able to correctly recognize a nested link and deal with escape brackets, it failed to correctly extract a link with nested parentheses. Right now, `getLinks` extracts whatever is inside the next open parenthesis and closed parenthesis without checking whether they are the same pair. A solution to this would probably be more involved and require me to create an algorithm similar to the stacks ADT or alternatively find some sort of way to count the number of open and closed parentheses to evaluate which indices correspond to a pair.

*My Peer's Implementation -- Failed*
![Image](labreport4-screenshots\labreport4-2.3b.png)
My peer's implementation of `markdown-parse` failed for snippet 2. Similar to my code, my peer's `getLinks` method does not take care of nested brackets or parentheses, which can be fixed with a more involved solution using the idea of the stacks ADT. However, just as I've mentioned in my peer's implementation of snippet 1, the problem of only extracting links following `](` returns. The escape brackets (closed) within the brackets mess up the code as it anticipates an open parenthesis next. Fixing the problem for escape brackets can be fixed by adding a simple `if` statement to disregard brackets with a `\` before them. However, the problem remains for nested brackets.

--
### **Snippet 3: New Lines in Brackets & Parentheses**
*Expected Output*
![Image](labreport4-screenshots\labreport4-3.1.png)
```
["https://ucsd-cse15l-w22.github.io/"]
```


*Creating a Test for this Snippet*
![Image](labreport4-screenshots\labreport4-3.2.png)


*My Implementation -- Failed*
![Image](labreport4-screenshots\labreport4-3.3a.png)
My implementation of `markdown-parse` failed for snippet 3. There are quite a few things in my code that needs to be fixed. As I've stated before, my `getLinks` method simply returns whatever is inside a set of open and closed parentheses given that they properly succeed a set of brackets. Thus, all of the line breaks gets returned as well. This can be fixed easily with the `String.trim()` method. However, a more involved solution is required for dealing with missing closed brackets or parentheses (mentioned earlier). When dealing with line breaks in between links, markdown only seems to create links given certain situations, such as a new line for the link itself or a one-line-break allowance when declaring a link. This can be solved by counting the number of line breaks when declaring the link and then proceeding if this number falls under markdown's allowance -- this definitely requires a more involved solution.

*My Peer's Implementation -- Failed*
![Image](labreport4-screenshots\labreport4-3.3b.png)
My peer's implementation of `markdown-parse` failed for snippet 3. The results of my peer's `getLinks` method is identical to mine. In fact, the solution to the problems proposed in my code also work for my peer's implementation of `markdown-parse`.