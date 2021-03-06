# Sociocracy 3.0 - A Practical Guide

This repository contains the source file for  a slide deck for teaching Sociocracy 3.0, currently available as 

* fast and mobile friendly static html pages: <http://patterns.sociocracy30.org>
* [online presentation](http://patterns.sociocracy30.org/slides.html)
* various other download formats, see  [sociocracy30.org/guide/](http://sociocracy30.org/guide/) 

German, Hebrew and French versions also exist and are also available via [sociocracy30.org/guide/](http://sociocracy30.org/guide/). If you want to help with translations into your language, please take a look at the [translations page](http://sociocracy30.org/translations/).

## Project Structure

- `content`: all the files that are uploaded to Crowdin for translation (or downloaded from crowdin to the translated repositories)
- `global`: files that are identical across languages, mostly templates, including some with translatable content that is collected in content/translations.pot, because Crowdin does not play nice with these files. Also contains not language-specific configuration file
- `config`: language-specific configuration files: project.yaml, make-conf, LaTEX styles etc
- `release`: the latest releasable builds (must be copied there manually, all build scripts deliver their output to the project root)
- `tmp` the Temporary folder is autogenerated by  `build.sh` or with `make setup`


## Build Process

`build.sh` builds all available targets, you can also use `make <target>` to build individual target.

The build process relies on [mdtools](https://github.com/bboc/mdtools) to prepare and compile the individual files, and on pandoc and LaTEX for epub formats.

Before the first target can be built, you need to run `make setup`, and the before building the static site adding or removing source files or illustrations it's a good idea to run `make clean`.

To set up a new language, run `make clean` and then copy over `content`, `global`, `config` and all files in the project root except for `crowdin.yaml` and `upload-translations.sh`. Adapt `build.sh` so it only contains targets that are available in that language (e.g. deckset makes no sense for RTL languages).

## Formats and Known Issues

The deck is currently available as PDF or PNG slides exported from [Deckset](decksetapp.com), as a html-version in [reveal.js](http://lab.hakim.se/reveal-js/#/) a static website (using jekyll and GitHub pages), and as e-books (ePub and PDF).

Deckset is nice to quickly hack together a beautiful presentation, but is a bit lacking when it comes to navigating larger presentations, and it's only available as a macOS app. Building the Hebrew version I discovered the hard way it does not support RTL languages., and did not find a way to automate pdf export, so with a growing number of languages Deckset is becoming increasingly painful. 

This is why I was looking at more open formats, and developed a generator for reveal.js, which generally works, but there might still a few small glitches in the CSS. Ping me if you find one. 

[Reveal.js docs](https://github.com/hakimel/reveal.js/blob/master/README.md)

Exporting to epub (via pandoc) and pdf via LaTEX is working, but still rough around the edges. The epub will benefit from a stylesheet and setting some [metadata for ibooks](http://pandoc.org/MANUAL.html#epub-metadata), while the styles for the pdf need some cleanup in all but the German versions.
 
## Markdown Styleguide

Information in this section is preliminary, and needs further testing.

The Markdown files for the individual patterns are grouped in directories per patterns group and built using a build script. Input format is Deckset 1 (for now), i.e. slide separators are "---". This will hopefully change in the future.

* Images always float right (because that works without clearing the float in reveal.js), and are set to height of 100%. Floating images go BEFORE the text, and are marked "right,fit"
* single images on slides: [inline,fit]
* Headline Level 1 is always the only content on the slide (apart from background images)
* Headline level 2  or more is increased by one for reveal.js
* within each pattern, the pattern title is headline level 2, all slides in patterns with a dedicated title need to use headline level 3, so it does not show up in the TOC on the website

## Updating reveal.js

Download zip from the [official repo](https://github.com/hakimel/reveal.js) and copy files over to `docs/reveal.js`. Diff `templates/revealjs-template.html` with `demo.html` to see if there are some changes to the basic html structure.

Keep (or adapt) `custom-styles.css` and `custom-theme.css` (derived from `css/theme/white.css`.

## Translations

Slides are translated in a [dedicated crowdin project](https://crowdin.com/project/sociocracy-30). The repository contains `crowdin.yaml` for use with the [crowdin CLI](https://support.crowdin.com/cli-tool/). 

Uploading sources is handled through this command (remove `--dryrun` to run):

`crowdin --identity ~/crowdin-s3-patterns.yaml --dryrun upload sources`

For each major revision we will create a branch with the version tag in crowdin, so future updates do not disrupt translation efforts:

`crowdin --identity ~/crowdin-s3-patterns.yaml upload sources -b {branch name} --dryrun`

The config file can be checked using 
`crowdin --identity ~/crowdin-s3-patterns.yaml lint`

 These commands assume [crowdin credentials](https://support.crowdin.com/configuration-file/#cli-2) in `~/crowdin-s3-patterns.yaml`


## License 

[![](http://creativecommons.org/images/deed/seal.png)](http://creativecommons.org/freeworks)

This slide deck is created by Bernhard Bockelbrink, James Priest and Liliana David, using illustrations from the [S3-Illustrations Repository](https://github.com/S3-working-group/s3-illustrations) by Bernhard Bockelbrink and [reveal.js](https://github.com/hakimel/reveal.js) by Hakim El Hattab.

_Sociocracy 3.0 -A Practical Guide_ is licensed to you under a **Creative Commons Free Culture License**. The exact license can be viewed [here](http://creativecommons.org/licenses/by-sa/4.0/).

Basically this license grants you

1. Freedom to use the work itself.
2. Freedom to use the information in the work for any purpose, even commercially.
3. Freedom to share copies of the work for any purpose, even commercially.
4. Freedom to make and share remixes and other derivatives for any purpose. 

You need to attribute the original creator of the materials, and all derivatives need to be shared under the same license. There's more on the topic of free culture on the [Creative Commons website.](http://creativecommons.org/freeworks)

