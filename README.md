# python-yacc-function-model
This is python-yacc function model. It combines files/functions in python-yacc in a single file.
It also promotes "multiple passes" concept.

## Multiple Passes
A standard method to parse a text of a language is to use two passes: a lexical pass and a syntactical pass.
The lexical pass transforms a text from a char string to a token string.
The syntactical pass takes the token string and transform to a boolean of acceptance and other results you want.

But you can have more passes.
For example, when parsing a Python text, the indentations are not easily handled in a lexical pass. You can add one or more passes, after the lexical pass and before the syntatical pass, to process the indentations of a Python text. So that after these passes, the token string satisfies a Context Free Grammar.

After, the processing of a text is just a sequence of transformation of a text. Each transformation can be a pass that transforms an input token string to an output token string.

Each pass can be described by a yacc spec file. In this folder we have *plex.txt* and *pyacc.txt*. They are the yacc spec file for the lexical pass and the syntactical pass (to process a text of yacc language).

Some trasformations are so small that we don't need to write it as a pass. Instead we just write it as a post-processing at the end of a pass.

## Structure of the File
The file *xparser.py* contains some basic functions that are used by all parsers.
It contains two *parse* functions one for each pass.

## Usuage
* To use the tool to build your own parser of a language of your choice, you make two copies of the file *xparser.py*.
* You design the number of passes you need to parse a text of the language. For each pass, you write a yacc spec file.
* You use one copy of *xparser.py* to process your yacc spec files. It generates codes from your yacc spec files. It also reports undefined terms in your yacc spec files.
* You use another copy of *xparser.py* as a model of your file parser program. Remove the two built-in parse functions. For each pass, your write your own *parse* function. In this parse function, you copy and paste the generated codes, and also define (write functions of) undefined terms. You may also do some post-processing in this function.
* Finally, you assemble these passes in the *run* function. Basically you piece up the parse functions you wrote.
