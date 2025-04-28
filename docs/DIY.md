# How to publish it yourself
This page assumes that you have some technical background. If that's not you, no problem! You may want to read the [publication overview](publication-overview.md) instead, which will allow you to customize a great deal without having to do anything technical.

## What do I need to understand?
This page assumes a very basic familiarity with GitHub and a working knowledge of XeLaTeX. If you're not familiar with XeLaTeX: it's a computer typesetting system that creates PDF files. There are plenty of resources online to learn, but it does have a rather steep learning curve. (If you have friends in mathematics, science, or engineering, they may be familiar with it.)

## The project repository
If you want to publish the books on your own, you'll want to get ahold of those files. There are two ways you can get to the GitHub repository:

1. The name of the repository follows a fixed format. It's always `pub-XXXXX` where `XXXXX` is the project ID. For instance, for the `bhsa` project, you can find the repository at [https://github.com/openreadersbibles/pub-bhsa](https://github.com/openreadersbibles/pub-bhsa).
2. From the “Projects” screen, click the “Advanced...” button and then “GitHub.” The repository's GitHub page will open in a new window.

## Types of files you'll find
The data for the project are stored in a SQL database in the cloud. During publication, the data for each book are put into two intermediate formats.

Different files are created for each book. The filenames have formats like `bhsa_OT_JON.xml`: `bhsa` is the project ID, `OT` is the canon, and `JON` is the book code (for Jonah). For the book of Jonah, we would get two data files:

1. `bhsa_OT_JON.json` contains raw(-ish) JSON data. (See “Using the TypeScript” below for help in using this.)
2. `bhsa_OT_JON.xml` is an XML representation of the book in [TEI format](https://tei-c.org/).

These files differ in their contents. The JSON file is more or less raw data from the database. There are columns that represent parsing data, for instance. The XML file, on the other hand, doesn't have all of the raw data but includes parsing information that is created by a particular [publication configuration](project-settings/publication-configurations.md). 

Here is the JSON content of a certain word in Obadiah 1:11:

```
    {
      "_id": 298325,
      "g_word_utf8": "שְׁבֹ֥ות",
      "trailer_utf8": " ",
      "voc_lex_utf8": "שׁבה",
      "gn": "unknown",
      "nu": "unknown",
      "st": "c",
      "vt": "infc",
      "vs": "qal",
      "ps": "unknown",
      "pdp": "verb",
      "freq_lex": 47,
      "gloss": {
        "type": "word",
        "_gloss": "take captive"
      },
      "qere_utf8": "",
      "kq_hybrid_utf8": "",
      "prs_gn": "NA",
      "prs_nu": "NA",
      "prs_ps": "NA",
      "reference": "OT OBA 1:11",
      "lex_id": 1438314,
      "phrasalGlosses": []
    },
```
You can see that the field `vt` (=verb tense) has `infc` (=infinitive construct). This is unformatted data.

The XML file, on the other hand, contains data that is specific to a particular publication configuration.

```
<w xml:id="id298325">שְׁבֹ֥ות</w>
<note type="gloss" n="b">
    <gloss type="parsing">G65</gloss>
    <gloss type="lexical-form">שׁבה</gloss>
    <gloss type="gloss">take captive</gloss>
</note>
```

The formatted parsing “G65” indicates a qal infinitive construct. The note marker “b” (from `n="b"`) comes from a publication configuration. A different project might format that parsing in a completely different way.

## Making TeX and HTML files
Then XSLT transformations are used to create `.tex` and `.html` files from the `.xml` file.

- `bhsa_OT_JON.html` is created by [tei2html.xsl](https://github.com/openreadersbibles/orb-server/blob/main/src/xslt/tei2html.xsl).
- `bhsa_OT_JON.tex` is created by [tei2tex.xsl](https://github.com/openreadersbibles/orb-server/blob/main/src/xslt/tei2tex.xsl).

Then a GitHub Action converts the `.tex` file into a PDF.

If you are investigating a problem in the build, you could also switch to the `gh-pages` branch of the repository, and examine the `bhsa_OT_JON.log` file.

## Using TypeScript
Even if you just want the data, it may be helpful to have the types that the project uses. The relevant repositories for managing the publication process are [orb-server](https://github.com/openreadersbibles/orb-server) and [models](https://github.com/openreadersbibles/models). If you want to do TypeScript development, you probably want the data in those files.

The relative paths in the files assume that `models` and `orb-server` are at the same level. E.g.,
```
/my-custom-project
/my-custom-project/models
/my-custom-project/orb-server
```

For instance, the `.json` file can be read and then used to create a [PublicationBook](https://github.com/openreadersbibles/models/blob/main/publication/PublicationBook.ts) object.

## Guide to the macros
Forthcoming...