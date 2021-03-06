# Syntax highlighter

Highlight the code in a frame.

## Install

Before running the script, you need to install the Python 2 version of [Pygments](http://pygments.org/).

You can install it with your package manager (in my case it did not pull in any dependency) or with Pip.

Using virtual environment will probably not work (well), since you will need to run Scribus after having activated it.

## Usage

Select the text frame with the code to be highlighted and run the script.

If Pygments cannot guess the language, create an item attribute (context menu > Attributes...) with named `syntax-highlight` with the language name as its value (see the [Pygment's languages list](http://pygments.org/docs/lexers/)).

## Notes

### The basic tokens to get started

Here is how a simple code is parsed into tokens:


```py
print("Hello World")
```

- Token.Keyword: print
- Token.Punctuation: () :
- Token.Literal.String.Double: " stringcontent
- Token.Text: space

```py
for i in range(3):
    print('Hello World')
```

- Token.Operator.Word: in
- Token.Name.Builtin: for
- Token.Literal.Number.Integer: 3

## Todo

- [x] Actually read the content of the frame
- [x] Optionally read the language from the item attributes
- [x] Make sure that the characte styles are reset before setting the new ones.
- [ ] Make sure that a text frame is selected.
- [ ] Allow highlighting a text selection.
  - Probably needs a new scripter API command.
- [x] Make sure that the character style `Code` is defined
- [x] Create the colors used by the highlither
  - Their names should be prefixed with `Code_`
- [ ] Create the character styles used for the specific code snippet
  - [ ] Create the styles with the default formatting defined by Pygments
	- [x] color
	- [ ] underline
	- [ ] bold
	- [ ] italic
  - [ ] Base the new styles on the `Code` style (needs a patch for `createCharStyle()`).
	- needs a patch for the `createCharStyle()` API command.
- [ ] Complete the matching between token types and styles
  - We don't want one style for each possible token type. Which types do we need?
- [ ] any way to create this as a c++ plugin?
  - https://doc.qt.io/qt-5/qtwidgets-richtext-syntaxhighlighter-example.html
	- but, then, i will probably have to recreate the lexers
