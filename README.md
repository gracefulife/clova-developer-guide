# Clova developer guide



## Introduction

This repository is created for managing and deploying [Clova developer guide](https://pages.oss.navercorp.com/JTF-P6/platform_technical_doc/) content. [GitBook](https://toolchain.gitbook.com/) is used for building document in PDF format and web format.

See the following sections for more details:

* [How to build documentation](#HowToBuild)
* [Branches](#Branches)
* [Releases](#Releases)

<a name="HowToBuild" />

## How to build documentation

Prepare the following tools and library:

* [`npm`](https://www.npmjs.com/get-npm)
* [`gitbook-cli`](https://toolchain.gitbook.com/setup.html)
* [`calibre`](https://toolchain.gitbook.com/ebook.html)

> Calibre library is required for building PDF. Make sure put the `ebook-convert` bin file to the $PATH.

> You can also make documentation build environment with Docker. See [Setup GitBook env. with Docker](https://oss.navercorp.com/JTF-P6/platform_technical_doc/wiki/Setup-GitBook-env-with-Docker)

To build a documentation, following next steps:

1. Clone this repository.

```bash
git clone https://oss.navercorp.com/JTF-P6/platform_technical_doc.git
```
2. (Required one time) Install required gitbook plugins.

```bash
gitbook install
```

3. Run one of following commands:

```bash
# If you want to make PDF file.
gitbook pdf . book.pdf

# If you want to make web content in ./book directory
gitbook build . book

# If you want to make web content with web server running on your PC
gitbook serve
```

<a name="Branches" />

## Branches

Due to the various purposes, this repository has the following branches:

* **master**
* **document**
* **gh-pages**
* **doc-KR**
* **doc-KR-Partner**
* **doc-KR-Partner-LGUplus**
* **doc-KR-En_Partner**
* **doc-JP**
* **doc-JP-ClovaHomeExt-Partner**
* **doc-JP-CustomExt-Partner**

> TBD : Add descriptions of the above branches


<a name="Releases" />

## Releases

The release history of Clova developer guide is recorded as GitHub issuse and release feature as below:

* [Issues with Deployment label](https://oss.navercorp.com/JTF-P6/platform_technical_doc/issues?utf8=%E2%9C%93&q=is%3Aissue%20label%3ADeployment%20)
* [Releases](https://oss.navercorp.com/JTF-P6/platform_technical_doc/releases)
