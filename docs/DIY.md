# How to publish it yourself
This page assumes that you have some technical background. If that's not you, no problem! You may want to read the [publication overview](publication-overview.md).

## What do I need to understand?
This page assumes a very basic familiarity with GitHub and a working knowledge of XeLaTeX. If you're not familiar with XeLaTeX: it's a computer typesetting system that creates PDF files. There are plenty of resources online to learn, but it does have a rather steep learning curve. (If you have friends in mathematics, science, or engineering, they may be familiar with it.)

## The Technical Details
The data for the project are stored in a SQL database in the cloud. For publishing, the relevant data are placed into a GitHub repository. Then a GitHub Action runs XeLaTeX on the `.tex` file. These are the steps:

1. The database is queried and all of the data are written to a JSON file.
2. This JSON file is then converted into a `.tex` file.
3. The GitHub Action converts the `.tex` file into a PDF.

If you want to publish the books on your own, you'll want to get ahold of those files. There are two ways you can get to the GitHub repository:

1. The name of the repository follows a fixed format. It's always `pub-XXXXX` where `XXXXX` is the project ID. For instance, for the `bhsa` project, you can find the repository at [https://github.com/openreadersbibles/pub-bhsa](https://github.com/openreadersbibles/pub-bhsa).
2. From the “Projects” window, click the “Advanced...” button and then “GitHub.” The repository's GitHub page will open in a new window.

Suppose you are interested in the `bhsa` project, and the OT book of Jonah. You'll probably be interested in these files:

- `bhsa_OT_JON.json` — The JSON data.
- `bhsa_OT_JON.tex` — The TeX file generated from the JSON file.
- `openreader.cls` — The LaTeX class file for the `.tex` file.

If you are investigating a problem in the build, you could also switch to the `gh-pages` branch of the repository, and examine the `bhsa_OT_JON.log` file.

## Guide to the macros
Forthcoming...