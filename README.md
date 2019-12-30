![Logo of the project](/docs/images/logo-sm.png)

# Verkilo™ (Pandoc Book)

[![Last Commit](https://img.shields.io/github/last-commit/merovex/verkilo-pandoc-book.svg)](https://github.com/merovex/pandoc-book/branches)
[![Compile Book(s)](https://circleci.com/gh/Merovex/verkilo-pandoc-book.svg?style=shield)](https://circleci.com/gh/Merovex/pandoc-book)
![Readme Compiler](https://github.com/Merovex/verkilo-pandoc-book/workflows/Compile%20Readme/badge.svg)

**Note:** Readme Auto-generated  (2019-12-30 14:11 UTC). Do not edit this file.

A brief description of your project, what it is used for and how does life get
awesome when someone starts to use it.

**Verkilo™ Pandoc Book** is my effort to create a Continuous Integration / Continuous Delivery (CI/CD) toolchain for book / document publication. I have a lifetime desire to write god-awful fiction, and a background in software development & project management.

## Contents

* [Use Cases](#use-cases)
* [Installing / Getting Started](#installing-getting-started)
* [Pandoc Bots (Docker Containers)](#pandoc-bots-docker-containers)
* [Configuration](#configuration)
  * [Trimsize](#trimsize)
  * [Fonts](#fonts)
* [Contributing](#contributing)
* [Links](#links)
* [Acknowledgements](#acknowledgements)
* [Licensing](#licensing)


## Use Cases

* **[Fiction Author](./docs/use-cases/fiction-author.md).** As an independent fiction author, you want to focus on writing, not formatting. Writing pays the bills. The typical author (See Alternatives) relies on a complex toolchain including Microsoft Word or Scrivener, Vellum, etc. that requires the author focus on non-revenue activities. Worse, they feel compelled to outsource this phase of production, which takes revenue away from the author. Pandoc Book (Verkilo™) provides professionally formatted, distribution-ready files in various formats.


## Installing / Getting Started

To use this template, clone the repository locally. Copy the contents of the `my-book/` directory as the new book you want to write (changing the name as appropriate). Then create a git repository of the new book.

You will need to install [Pandoc](https://pandoc.org/), and be familiar with [Markdown](https://daringfireball.net/projects/markdown/).

Commands you can execute:

* `make clean` - Deletes content of `build/`
* `make docx` - Converts the Markdown in `text/` to Word DOCX format (output placed in `build/` directory).
* `make html` - Converts the Markdown in `text/` to HTML format (output placed in `build/` directory).
* `make mobi` - Converts the Markdown in `text/` to MOBI format (output placed in `build/` directory).
* `make pdf` - Converts the Markdown in `text/` to PDF format (output placed in `build/` directory).

Pandoc Novel uses the [git tag](https://git-scm.com/book/en/v2/Git-Basics-Tagging) for the version added in the metadata and the filename. This is useful to keep track of different versions of the same work (i.e., different drafts; releases to editors, beta readers, etc. )

* `git tag -a v1.4 -m "my version 1.4"`

## Pandoc Bots (Docker Containers)

<!-- pandoc-book-compile -->
**Pandoc Book Compile** is a Docker container that auto-generates books using Pandoc and pushes them to an active release on Github.
[Read more](./pandoc-book-compile/README.md)
<!-- /pandoc-book-compile -->

<!-- pandoc-book-readme -->
**Pandoc Book Readme** is a Docker container that auto-generates a compound README from Markdown files within the repository. It looks for all content between two comment tags, then inserts them in a README based on a template.
[Read more](./pandoc-book-readme/README.md)
<!-- /pandoc-book-readme -->

## Configuration

At a minimum, you will want to review / edit the following attributes in the `metadata.yml` file:
* `title` - The title of the book
* `subtitle` - The subtitle of the book
* `author` - The author(s) of the book (can be a string or array)
* `website` - The author's website
* `other-titles` - An array of other titles the author wants the reader to be aware of
* `rights` - The work's copyright statement
* `disclaimer` - The author's disclaimer
* `reservation` - The author's reservation of rights
* `isbn` - An array of ISBNs associated with the underlying work
* `identifier` - The ISBN associated with the EPUB
* `credits` - An array of those who supported the books' publication (artists, authors)

The `images/` directory is where you should place images used to support the published work. You will also want to replace the following images with your own:
* `cover.png` Provides the cover for the epub.
* `logo.png` Provides the imprint logo (both the name and logo are registered trademarks).

The `text/` directory is where Pandoc Novel looks for the Markdown content.

<!-- trimsize -->
### Trimsize

The PDF option includes multiple trim sizes, depending on your target form factor. The Word document has a fixed trim size (Letter). The ePUB and HTML lack trim sizes. Metric measures rounded to 2 digits in the table. All measures are in metric in the LaTeX macros. (US Customary Measures are defined by their Metric equivalent.) When calculating trim size, we compared [commonly used sizes](./trim-sizes.md) and those offered by [KDP](https://kdp.amazon.com/en_US/help/topic/G201834180#trim).

|   Trimsize       |   Paper Size    |
|        ---       |       :---:     |
| **Letter**       | 8-1/2" x 11"    |
| **LargeTrade**   |     8" x 10"    |
| **Textbook**     |     7" x 10"    |
| **Trade**        |     6" x 9"     |
| **Digest**       | 5-1/2" x 8-1/2" |
| **SmallTrade**   | 5-1/4" x 8"     |
| **Novella**      |     5" x 8"     |
| **AFourSize**    |   21cm x 30cm   |
| **UKAFormat**    |   11cm x 18cm   |
| **UKBFormat**    |   13cm x 20cm   |

* Top and Inner margins are 2cm (~3/4").
* Outer and bottom margins are 17mm (~5/8").
* When attribute `bleed: true` is set, then the paper size and margins are increased by 3mm wide and 6mm high. (I don't think we can bleed an image, though.)
* Set attribute `crop: true` to see what a given size looks like scaled properly on a letter-sized printout.

**Warning:** Failure to use one of the listed trim sizes will cause the compilation to fail. Defaults to `trimsize: Trade`.
[Read more](./docs/configuration/trimsize.md)
<!-- /trimsize -->

<!-- fonts -->
### Fonts

Verkilo configures three default fonts, but you may reconfigure them provided they are available when using the LaTeX font packages listed here. See [Pandoc fonts for LaTeX](https://pandoc.org/MANUAL.html#fonts) for more information.

Fonts are configured in either the `metadata.yml` or the in-document Frontmatter.

The LaTeX packages used for font assignments are:

```
\usepackage{fontspec}
\usepackage{xunicode}
\usepackage{xltxtra}
```

| Family | Default | Attribute |
| :-: |  :-: | :- |
| Serif       | Libre Baskerville | seriffont: Libre Baskerville |
| Sans-Serif  | Libre Franklin    | sansfont: Libre Franklin |
| Monospace   | Inconsolata       | monofont: Inconsolata  |

**Why default Baskerville, Franklin & Inconsolata?** Both Libre Baskerville and Libre Franklin have been optimized for use on screen. Baskerville is nice and readable, so ideal for use as body text, while Franklin is better suited to headlines. Inconsolata pairs with Baskerville & Franklin as they all share similar traits (double-story g & a, etc.). See the [Libre Baskerville / Franklin / Inconsolata pairing image](./images/libre-franklin-baskerville-inconsolata.png).

Here is an example of customizing fonts based on the Source Pro series:

```
seriffont: "Source Serif Pro"
sansfont: "Source Sans Pro"
monofont: "Source Code Pro"
```
[Read more](./docs/configuration/font.md)
<!-- /fonts -->
<!-- fonts -available-->

## Contributing

If you'd like to contribute, please fork the repository and use a feature
branch. Pull requests are warmly welcome. See [Contributions](/CONTRIBUTING.md) for more information.

## Links

Even though this information can be found inside the project on machine-readable
format like in a .json file, it's good to include a summary of most useful
links to humans using your project. You can include links like:

<!-- - Project homepage: https://your.github.com/awesome-project/ -->
- Repository: https://github.com/Merovex/pandoc-book/
- Issue tracker: https://github.com/Merovex/pandoc-book/issues
- Related projects:
  - Your other project: https://github.com/your/other-project/
  - Someone else's project: https://github.com/someones/awesome-project/

## Acknowledgements

My earlier forays into plaintext to Novel were in LaTeX, then a [custom-modified Ruby approach](https://github.com/Merovex/verku). This toolchain is a pivot to an automated toolchain and its inspiration owes appreciation to:

* Scott Selisker, [A Plain Text Workflow for Academic Writing with Atom](http://u.arizona.edu/~selisker/post/workflow/) & KDheepak, [Writing Technical Papers with Markdown](https://blog.kdheepak.com/writing-papers-with-markdown.html). Both encouraged me to re-build a toolchain.
* Dennis Tenen and Grant Wythoff, [Sustainable Authorship in Plain Text using Pandoc and Markdown](https://programminghistorian.org/en/lessons/sustainable-authorship-in-plain-text-using-pandoc-and-markdown), for encouraging me to focus on Pandoc for the toolchain.
* Pascal Wagler, [Eisvogel](https://github.com/Wandmalfarbe/pandoc-latex-template), for giving away that one can pull down the stock Pandoc LaTeX template and modify it.
* BP, [Pandoc Google Group](https://groups.google.com/forum/?utm_medium=email&utm_source=footer#!msg/pandoc-discuss/JVAKdezOoVg/RCY30ypTEQAJ), for helping me change the Horizontal Rule into a Plain Fancy Break.
* [Memoir class](https://ctan.org/pkg/memoir?lang=en), for having code on Plain Fancy Break that I was able to copy over.

## Licensing

The code in this project is licensed under a BSD-4 [license](./LICENSE.md).