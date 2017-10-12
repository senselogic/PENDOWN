![](https://github.com/senselogic/PENDOWN/blob/master/LOGO/pendown.png)

# Pendown

Lightweight markup for colored documents.

## Features

* Simple, concise and consistent syntax to quickly write colored documents.
* Complete : styles, colors, alignments, page breaks, links, lists, code blocks, tables, quotes, frames and images.
* Fast conversion to HTML by a standalone command line tool or by a web browser script.
* The generated files can be loaded in LibreOffice Writer.
* Source code syntax highlighting.

## Getting Started

Install the Pendown installation files in a local folder on your computer, and open the "sample.html" file with a plain text editor like Geany or Notepad++.

You will see that all its text is written using Pendown tags, which are automatically converted on-the-fly when the HTML file is opened.

```html
<meta charset="utf8"/>
<link rel="stylesheet" href="../pendown.css">
<xmp>
! Title

**Pendown** tags are automatically converted into **HTML** tags when the file is opened in a web browser.

---

!! Line break

Manual line break§
inside a paragraph.

Another paragraph.

!! Page break

~~~

This is printed on a new page.

!! Escape

\_\_

`** <b>not bold</b> **`

!! Alignment

<<left<<

$$center$$

>>right>>

!! Styling

**bold**

%%italics%%

^^superscript^^

,,subscript,,

~~strikethrough~~

~~f00\strikethrough~~

__underlined__

__f00\underlined__

##highlighted##

##fce\highlighted##

{{0cc\colored}}

{{6f42c1\colored}}

°°black°°

¹¹cyan¹¹

²²orange²²

³³green³³

°gray°

¹pink¹

²red²

³blue³

!! Block

{{{
Block
}}}

{{{cfe\
Block
}}}
    
!! Box

###
Box
###

###cfe\
Box
###

!! Frame

+++
Frame
+++

+++f00\
Frame
+++

{{{ffd\
+++f00\
Frame
+++
}}}

!! Quote

>>>
Quote
>>>

>>>f00\
Quote
>>>

{{{ffd\
>>>f00\
Quote
>>>
}}}

!! Table

%%%
      |Monday|Tuesday|Wednesday
Apple |1     |2      |3
Orange|1     |2      |3
Banana|1     |2      |3
%%%

!! Code

:::
##// ²Colorized source code²##

²if² ³(³ ... ³)³
³{³
    ...
³}³
²else²
³{³
    ...
³}³
:::

:::c++\
// Colorized source code

#include <iostream>

using namespace std;

int main() 
{
    cout << "Hello world!";
    
    return 0;
}
:::

!! List

Four spaces per level.

*   List
*   List
    *   Sub-list
    *   Sub-list
    #   Numbered sub-list
    #   Numbered sub-list
        #   Numbered sub-list
        #   Numbered sub-list
    #   Numbered
        sub-list
*   List§
    ...

!! Link

@@http://www.github.com This is a link@@

@@http://www.github.com [[20:image.jpg]]@@

@@http://www.github.com@@

!! Image

Small :

[[20:image.jpg]][[20:image_2.jpg]]§
[[20:image_3.jpg]][[20:image_4.jpg]][[20:image_5.jpg]]

Medium :

[[40:image_3.jpg]][[40:image_4.jpg]]

Large :

[[image.jpg]]§
[[:image_2.jpg]]§
[[,100:image_4.jpg]]

Custom :

[[50vw,50%:image_5.jpg]]

!! HTML

²Pendown tags² can be mixed with <span style="color:green">HTML tags</span>.
</xmp>
<script src="../pendown.js"></script>
```

Then open the "sample.html" file with a web-browser.

You should see the following result if the Comic Sans and Consolas fonts are already installed on your system.

![](https://github.com/senselogic/PENDOWN/blob/master/SAMPLE/sample.png)

## Syntax highlighting

The source code programming language can be specified with the following keywords :

* C : c h
* C++ : c++ h++ cpp hpp cxx hxx
* C# : c# cs
* D : d
* Java : java
* JavaScript : js
* TypeScript : ts

When colorizing a source code file, its programming language is deduced from the file extension if it matches one of the above keywords.

## Client-side compiler

### Installation

Just put the "pendown.css" and "pendown.js" files in the same folder as your HTML files, or in a folder accessible from them.

### Usage

Write your Pendown text inside the `<xmp>` section.

```html
<meta charset="utf8"/>
<link rel="stylesheet" href="pendown.css">
<xmp>
$$Hello world !$$
</xmp>
<script src="pendown.js"></script>
```

### Troubleshooting

> The Pendown page doesn't show the converted text.

Check that the Pendown file extension is ".html".

Check that your text is between the `<xmp>` and `</xmp>` tags.

Check that the relative paths to "pendown.css" and "pendown.js" are correct.

> The Pendown page doesn't use the Comic Sans MS or Consolas font as in the "sample.png" image.

Check that both fonts are properly installed on your system.

> The Pendown page doens't apply the page breaks in the browser.

They are applied when printing the page from the browser, or when the generated file is loaded in LibreOffice Writer.

### Frequently asked questions

> How can I force Pendown to use black as the default text color ?

Replace `<xmp>` by `<xmp class="black">` in the HTML file.

> How can I hide the Pendown text until it has been converted into HTML ?

Replace `<xmp>` by `<xmp style="display:none">` in the HTML file.

## Server-side compiler

### Installation

Install the [DMD 2 compiler](https://dlang.org/download.html).

Build the executable with the following command line :

```bash
dmd -m64 pendown.d
```

### Command line

```bash
pendown [options] input_file output_file
```

### Options

```
--colorize : generate a Pendown file from a source code file
--process : generate a HTML file from a Pendown file
--loadable : make the HTML file loadable in LibreOffice Writer
--script : make the HTML file import the Pendown script file
--style : make the HTML file import the Pendown style file
--language c|c++|cpp|c#|cs|d|java|js|ts : set the source code language
--tabulation 4 : set the text tabulation space count
--indentation 4 : set the list indentation space count
--path PENDOWN_FOLDER/ : set the path of the imported Pendown files 
``` 

### Examples

```bash
pendown --process --style --path ../ document.pd document.html
```

Converts a Pendown file to a HTML file which imports the Pendown style file.

```bash
pendown --process --loadable --style --path ../ document.pd document.html
```

Converts a Pendown file to a HTML file which can be loaded in LibreOffice Writer.

```bash
pendown --script --style --path ../ document.pd document.html
```

Converts a Pendown file to a HTML file which imports the Pendown script and style files to convert the Pendown tags inside the web browser.

```bash
pendown --colorize code.d code.pd
```

Converts a D source code file to a Pendown file.

```bash
pendown --colorize --process --style --path ../ code.d code.html
```

Converts a D source code file to a HTML file which imports the Pendown style file.

```bash
pendown --colorize --script --style --path ../ code.d code.html
```

Converts a D source code file to a HTML file which imports the Pendown script and style files to convert the Pendown tags inside the web browser.

## Limitations

* Lists are not processed inside preformatted blocks.
* The Pendown text can't contain the string `</xmp>` when it is converted by the web browser script.

## Version

1.0

## Author

Eric Pelzer (ecstatic.coder@gmail.com).

## License

This project is licensed under the GNU General Public License version 3.

See the [LICENSE.md](LICENSE.md) file for details.
