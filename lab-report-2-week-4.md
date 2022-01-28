# Week 4 - Lab Report 2
## ***FIXING BUGS IN A PROGRAM***

#### In this lab, you will see 3 code changes in `markdown-parse` to learn more about bugs, symptoms, and failure-inducing inputs.
---
### **Code Change #1**: Parentheses Inside Brackets
![Screenshot](labreport2-screenshots/labreport2-1.png)
- [Link to failure-inducing input](https://github.com/aliu104/markdown-parse/blob/main/faulty-file1.md)
- Program symptom:
```
> javac MarkdownParse.java
> java MarkdownParse faulty-file1.md
```
- The failure inducing input is a file with a set of parentheses inside a set of brackets. The bug here comes from the program's inability to find parentheses after the closing bracket. This causes the symptom of an infinite loop as the program attempts to access characters in the string that aren't there.

--
### **Code Change #2**: No Closing Bracket
![Screenshot](labreport2-screenshots/labreport2-2.png)
- [Link to failure-inducing input](https://github.com/aliu104/markdown-parse/blob/main/faulty-file2.md)
- Program symptom:
```
> javac MarkdownParse.java
> java MarkdownParse faulty-file1.md
```
- The failure inducing input is a file with an opening bracket, set of parentheses, but no closing bracket. The bug here comes from the program's inability to find the closing bracket anywhere in the file. This causes the symptom of an infinite loop as the program attempts to access the closing bracket, which doesn't exist.

--
### **Code Change #3**: No Closing Parenthesis
![Screenshot](labreport2-screenshots/labreport2-3.png)
- [Link to failure-inducing input](https://github.com/aliu104/markdown-parse/blob/main/faulty-file3.md)
- Program symptom:
```
> javac MarkdownParse.java
> java MarkdownParse faulty-file3.md 
Exception in thread "main" java.lang.StringIndexOutOfBoundsException: begin 34, end -1, length 56
        at java.base/java.lang.String.checkBoundsBeginEnd(String.java:3756)
        at java.base/java.lang.String.substring(String.java:1902)
        at MarkdownParse.getLinks(MarkdownParse.java:26)
        at MarkdownParse.main(MarkdownParse.java:43)
>
```
- The failure inducing input is a file with a set of brackets, an opening parenthesis, but no closing parenthesis. The bug here comes from the program's inability to find the closing parenthesis anywhere in the file. This causes the symptom of an index out of bounds exception as the program attempts to utilize the substring method.