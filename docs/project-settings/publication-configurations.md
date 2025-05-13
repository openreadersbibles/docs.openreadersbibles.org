# Project Settings
## Publication Configurations

These are settings for how your book will look when it is published. 

If you want to publish books in several different formats, see “Add a new publication configuration” below.

## Select the parsing formats to use when publishing
For each canon, you need to select the parsing format you want to use. If you haven't created a parsing format for a particular canon, you need to do that first in the [Parsing Formats](parsing-formats.md) section.

## Font/language settings
These are settings that make sure the book is typeset appropriately for your language.

## Select the typography language
If your language is in the list, then just choose it.

If your language is not in the list, then select the language whose documents look most like your language. For instance, if you write your language with the Cyrillic script, you might select “russian”. (You definitely want the script to match. You might be able to get closer; for instance both “russian” and “bulgarian” are options.)

Technical detail you don't need to worry about: this is the language used by the [polyglossia](https://ctan.org/pkg/polyglossia?lang=en) LaTeX package.

## Select the font for your language
Choose the font that you want to use for your language. These are fonts that are available with open licenses. You can go to the [Google Fonts](https://fonts.google.com/) to see samples. See [Fonts](../fonts.md) for a little more detail.

Using Google Fonts lets us automate the documentation creation project, and avoids concerns about copyright. If for some reason you need a font that is not part of Google Fonts, you can make it work, but it will be harder. See the [do-it-yourself](../DIY.md) guide.

## Use SBL BibLit for the biblical text
Using the SBL BibLit font is a really good idea. It is an attractive typeface and free. But if you want to use a different one, you can untick this box and select a Google Font instead.

## Chapter Headers
This is a template so that you can create your language's equivalent of “Chapter 15”. In this template “\__CHAPTER__” will be replaced by the chapter number.

In right-to-left languages, this is going to be awkward. Here is how I would do it:

1. Copy the text “\__CHAPTER__” to the clipboard (without the quotes).
2. Remove all the text from the text box.
3. Type in your “chapter” equivalent.
4. Place your cursor where you want the chapter number to go (remember to include a space, if needed).
5. Paste the text from the clipboard.
6. Check in the “Example” below that it looks right. 

## Footnotes
This section is about what your footnote markers look like, i.e., the thing that comes after a word and tells you there is a footnote^a to look at.

The reader's bibles we have seen seem to take two approaches to footnotes:

- Footnotes are indicated by letters (a, b, c, ...). The letters restart at the beginning of each verse.
- Footnotes are numbered. The numbering restarts on the page.

(The advantage of using letters is that the footnote markers look very different from verse numbers.)

### If you're doing letters, how many footnote markers do you need?
This will depend on the frequency threshold. The lower your threshold, the more words in a verse will need a gloss. As an example, if your frequency threshold for the Old Testament was 50, then you would need 31 different footnote markers. (That is for Daniel 3:15 — a very long verse that's in Aramaic.) If your frequency threshold was 100, then you would still need just 31 different footnote markers.

If we run out of footnote markers, we start back at the beginning. So if you only specify “a,b,c,d,e” then the order of footnotes would be: “a,b,c,d,e,a,b,c,d,e,a,b,c,d,e,...”. (That may not be bad; maybe your readers would able to figure it out.)

Another strategy is to use doubled letters after you've gone through all of the alphabet: “a,b,c,d,e...,x,y,z,aa,bb,cc,dd,ee...”.

## Custom Frequency Thresholds (advanced)
One way you can customize a publication is by changing the frequency thresholds. You can use lower thresholds (i.e., providing less information to the reader) to produce editions for more advanced readers.

The caution of course is that if these thresholds are higher than what you have set for your project, then there will just be blanks rather than glosses, because you haven't entered the glosses for them.

## LaTeX template (advanced)
If you're a LaTeX user, you can use this to customize the `.tex` file that is used to build your PDFs. This allows you to customize your PDFs without going full [DIY](../DIY.md). You probably want to consult that guide, however, and the project's repository, to figure out the best way to modify this file.

## CSS template (advanced)
You can change the CSS template that is used for the webpage version (HTML version) of the book. Specifically, the CSS on the website will be [this file](https://github.com/openreadersbibles/publication-files/blob/main/style.css) plus whatever you put in your CSS template. (What comes later in the CSS file has priority, so your changes will override whatever else in in that file.)

These placeholders will be replaced with the fonts specified in the project settings:

- `__BIBLICAL_FONT__` E.g., `SBL BibLit`
- `__PROJECT_FONT__` E.g., `Charis SIL`
- `__LAYOUT_DIRECTION__` E.g., `rtl` or `ltr` (this is the layout direction of the project language, e.g., Russian or Swahili)

## Add a new publication configuration
At first you just have the “default” publication configuration. One project can have multiple publication configurations, however. 

- You could have an edition with short parsing formats (e.g., G20) for advanced readers, and a different one with long parsing formats (e.g., qal imperfect third masculine singular) for beginning readers.
- You could have editions for A4 paper and Letter paper.
- ...or any other of the settings people might disagree about!

You can click “Add a new publication configuration” to create as many as you wish. It's good idea to have a computer-friendly name for the name of the configuration (e.g, “a4paper-long-format”).

