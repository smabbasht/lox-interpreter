## Challenge 1

1. There are at least six domain-specific languages used in the little system I
   cobbled together to write and publish this book. What are they?

These are the ones I saw in the repo linked:
- HTML is one such ^domain-specific^ or little language that is being used as a
  markup language.
- CSS is another one that is being used for styling.
- Dart is yet another little language designed for making mobile and web-apps.
- SCSS is another styling little language but is a pre-processor scripting
  language with variables, nesting, and functions, which makes it easier to
  manage larger projects. 
- Make makes defining the build, run, clean and other directives very easy and
  is another such little language written in Makefile.
- Markdown is another DSL helps to write using an easy-to-read, easy-to-write
  plain text format, language that converts to structurally valid HTML/XHTML.

2. Get a “Hello, world!” program written and running in Java. Set up whatever
   makefiles or IDE projects you need to get it working. If you have a
   debugger, get comfortable with it and step through your program as it runs.

I use NeoVim as an IDE/editor which I have already configured with files
[linked](https://github.com/smabbasht/nvim). I have LSP for java installed
and a debug adapter that allows me to use the debugger for java inside my IDE.

the hello world program in Java is attached below from file `hello.java`
```java
public class hello {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

The code can be compiled with:
```sh 
javac hello.java
java hello
```

