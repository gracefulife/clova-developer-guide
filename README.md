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

> Calibre application is required for PDF documentation build. Make sure put the `ebook-convert` bin file to the $PATH contained in Calibre application.

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

# If you want to run web server with GitBook web content. You can access the web server at http://localhost:4000.
gitbook serve
```

<a name="Branches" />

## Branches

Due to the various purposes, this repository has the following branches:

<ul>
  <li><strong>document</strong><br />Main branch that holds whole content of Clova developer guide. Working branches are forked from this branch and after job is done the branches are merged back to this branch.</li>
<li><strong>doc-JP</strong><br />Branch for Japanese business, this branch holds EN version documentation. JA version will be added future. (document -> doc-JP)
<li><strong>doc-JP-ClovaHomeExt-Partner</strong><br />Branch for Japanese partners who provides IoT services via Clova. (doc-JP -> doc-JP-ClovaHomeExt-Partner)
<li><strong>doc-JP-CustomExt-Partner</strong><br />Branch for Japanese partners who provides extensions via Clova. (doc-JP -> doc-JP-CustomExt-Partner)
<li><strong>doc-KR</strong><br />Branch for Korean business, this branch holds KO and EN version documentation. (documnt -> doc-KR)
<li><strong>doc-KR-En_Partner</strong><br />Branch for Korean partners who prefer English such as Xaomi. (EN, PDF doc, doc-KR -> doc-KR-En_Partner)
<li><strong>doc-KR-Partner-LGUplus</strong><br />Branch for LG Uplus (Korean partner) contains LG Uplus exclusive specification. (KO, TV STB exclusive spec., PDF doc, doc-KR -> doc-KR-Partner-LGUplus)
<li><strong>doc-KR-Partner</strong><br />Branch for Korean partners contains partner exclusive specification. (KO, PDF doc, doc-KR-Partner-LGUplus -> doc-KR-Partner)
<li><strong>doc-KR-Public</strong><br />Branch for public documentation which is deployed on NAVER developer center. (KO, online doc, doc-KR-Partner -> doc-KR-Public)
<li><strong>master</strong><br />Backup branch for <strong>document</strong> branch (document -> master)
<li><strong>gh-pages</strong><br />Web content for internal use (http://pages.oss.navercorp.com/JTF-P6/platform_technical_doc).
</ul>

<a name="Releases" />

## Releases

The release history of Clova developer guide is recorded as GitHub issuse and release feature as below:

* [Issues with Deployment label](https://oss.navercorp.com/JTF-P6/platform_technical_doc/issues?utf8=%E2%9C%93&q=is%3Aissue%20label%3ADeployment%20)
* [Releases](https://oss.navercorp.com/JTF-P6/platform_technical_doc/releases)

> Due to translation job, EN version documentation is released after 1 or 2 week(s).
