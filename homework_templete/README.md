## My Latex Homework Templete

This is the latex homework templete used by me in the universities. It provides some simple features to manage your answers simply and cleanly.  

```
\name{} # name of the author.
\course{} # name of the course.
\term{} # current term.
\hwnum{} # the number of current homework
```

### Usage

- The simplest way to use this templete is that you put .cls in the same directory as your latex source and compile with latex.  
- We recommend you to add this to your sharing templete in your system.
-- I am not a Windows user, please explore yourself on Windows on how to use Latex gracefully.   
-- For Linux users, you may create a new directory, put ".cls" to this directory and add this path into **TEXINPUTS**.
```
export TEXINPUTS="/your/path:$TEXINPUTS"
```
Then this will enable you to use it everywhere on your computer.
