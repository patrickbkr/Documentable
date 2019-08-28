# Documentable, the Perl6 Doc API [![CI Status](https://circleci.com/gh/perl6/Documentable.svg?style=shield)](https://circleci.com/gh/antoniogamiz/Perl6-Documentable) [![Build Status](https://travis-ci.org/antoniogamiz/Perl6-Documentable.svg?branch=master)](https://travis-ci.org/antoniogamiz/Perl6-Documentable) [![artistic](https://img.shields.io/badge/license-Artistic%202.0-blue.svg?style=flat)](https://opensource.org/licenses/Artistic-2.0)

In this repository you can find all logic responsible of generate the [official documentation of Perl6](https://docs.perl6.org/) or any other repository that follows the same specification. Could be used for modules that include a substantial amount of documentation, for instance.

## Table of contents

- [Installation](#installation)
- [Usage](#usage)
- [Documentation](https://antoniogamiz.github.io/Perl6-Documentable/)
- [Docker container](#docker-container)
- [Default templates](#default-templates)
- [Tests](#ŧests)
- [FAQ](#faq)
- [Authors](#authors)

## Installation

```
$ zef install Perl6::Documentable
```

If you have already downloaded this repo,

```
$ zef install .
```

## Usage

Before generating any documents you should execute:

```
documentable setup
```

in order to download the necessary files needed to generate the site (CSS, svg, ...). Alternatively, you can add your own. See [default templates](#default-templates) to get more information.

```
Usage:
  bin/documentable setup -- Downloads default assets to generate the site
  bin/documentable start [--topdir=<Str>] [--conf=<Str>] [-v|--verbose] [-c|--cache] [-p|--pods] [-k|--kind] [-s|--search-index] [-i|--indexes] [-t|--type-images] [-f|--force] [--highlight] [--typegraph-file=<Str>] [--highlight-path=<Str>] [--dirs=<Str>] [-a|--all] -- Start the documentation generation with the specified options
  bin/documentable update [--topdir=<Str>] [--manage] [--conf=<Str>] -- Check which pod files have changed and regenerate its HTML files.
  bin/documentable clean -- Delete files created by "documentable setup"

    --topdir=<Str>            Directory where the pod collection is stored
    --conf=<Str>              Configuration file
    -v|--verbose              Prints progress information
    -c|--cache                Enables the use of a precompiled cache
    -p|--pods                 Generates the HTML files corresponding to sources
    -k|--kind                 Generates per kind files
    -s|--search-index         Generates the search index
    -i|--indexes              Generates the indexes files
    -t|--type-images          Write typegraph visualizations
    -f|--force                Force the regeneration of the typegraph visualizations
    --highlight               Highlights the code blocks
    --typegraph-file=<Str>    TypeGraph file
    --highlight-path=<Str>    Path to the highlighter files
    --dirs=<Str>              Dirs where documentation will be found. Relative to :$topdir
    -a|--all                  Equivalent to -t -p -k -i -s
    --manage                  Sort Language page
```

See the [CLI documentation](https://antoniogamiz.github.io/Perl6-Documentable/language/cli) to learn more.

## Default templates

As you may have noticed, every page in the documentation follows the
same template. You can get those templates in
the
[releases page](https://github.com/antoniogamiz/Perl6-Documentable/releases/tag/v1.1.2). I
strongly recommend you to use the defaults, which can be set up executing

```
documentable setup
```

That command will download
the
[latest assets tarfile](https://github.com/antoniogamiz/Perl6-Documentable/releases/download/v1.1.2/assets.tar.gz) in
your directory. But what does this tar contain? Several things:

- Necessary files to enable highlighting (`highlights` dir).
- `html` dir containing several icons, graphics, etc. In this directory will be written all HTML documents generated by `Perl6::Documentable`.
- `assets` dir containing the style sheets used and JS code to enable search functionality.
- `template` dir containing the default templates used.
- Two files to run the server (`app-start` and `app.pl`).
- A Makefile to configure highlighting (`make init-highlights`) and easily start a dev server with `make run`.

## Docker container

There is a specific docker container with all necessary dependencies (including the highlighter) at https://github.com/antoniogamiz/docker-documentable.

You can see an example about how to use it [here](https://github.com/antoniogamiz/Perl6-Documentable/blob/master/.circleci/config.yml).

## Installing dependencies

#### Rakudo

You need Perl 6 installed. You can install the Rakudo Perl 6 compiler by
downloading the latest Rakudo Star release from
[rakudo.org/downloads/star/](http://rakudo.org/downloads/star/).

#### `zef`

[Zef](https://modules.perl6.org/repo/zef) is a Perl 6 module installer. If you
installed Rakudo Star package, it should already be there. Feel free to
use any other module installer for the modules needed (see below).

#### Mojolicious / Web Server (OPTIONAL)

Mojolicious is written in Perl 5, so assuming that you use
[`cpanm`](https://metacpan.org/pod/App::cpanminus),
install this now:

```
    $ cpanm -vn Mojolicious
```

#### GraphViz

To generate the svg files for the typegraph representation you need to have installed `graphviz`. If you use Ubuntu/Debian:

```
    $ sudo apt-get install graphviz
```

#### Highlight (OPTIONAL)

This is necessary to appli highlighting to the code examples in the documentation. You can skip it, but have in mind that all code examples will appear with the same color (black).

You can set this up with the default Makefile (obtained using `documentable setup`):

```
    make init-highlights
```

#### SASS Compiler

To build the styles, you need to have a SASS compiler. You can either install
the `sass` command

```
    $ sudo apt-get install ruby-sass
```

#### wget and tar

This programs are used by `documentable setup` to download the default assets and extract them. If you are on Ubuntu/Debian you will not have any problem (probably). If you are using Windows I recommend you to download the assets yourself from [this link](https://github.com/antoniogamiz/Perl6-Documentable/releases/download/v1.1.2/assets.tar.gz).

## FAQ

_Question:_ Do I need to regenerate all pages when I have only changed one?

_Answer:_ No, you can execute `documentable update` to only regenerate those pages affected by your changes.

##

Is not your question here? Then, please [raise an issue](https://github.com/antoniogamiz/Perl6-Documentable/issues/new).

# AUTHORS

Antonio Gámiz Delgado <@antoniogamiz>

Moritz Lenz <@moritz>

Jonathan Worthington <@jnthn>

Richard Hainsworth<@finanalyst>

Will Coleda <@coke>

Aleks-Daniel <@AlexDaniel>

Sam S <@smls>

Juan Julián Merelo Guervós <@JJ>

MorayJ <@MorayJ>

Zoffix <@zoffixnet>

Tison <@TisonKun>

Samantha Mcvey <@samcv>

Altai-Man <@Altai-man>

Tom Browder <@tbrowder>

Alexander Moquin <@Mouq>

Wenzel P. P. Peppmeyer <@gfldex>

# COPYRIGHT AND LICENSE

Copyright 2019 Perl6 Team

This library is free software; you can redistribute it and/or modify it under the Artistic License 2.0.

This module uses some conventions: (this started in August, 2019, so previous work does not follow the conventions):

- [Semantic Versioning](https://semver.org/).
- [Branching model](https://nvie.com/posts/a-successful-git-branching-model/).
- [Commit names](https://chris.beams.io/posts/git-commit/).

We use a [ChangeLog generator](https://github.com/github-changelog-generator/github-changelog-generator) to generate the [CHANGELOG.md file](CHANGELOG.md).
