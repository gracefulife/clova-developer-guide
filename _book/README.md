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

3. Run one of the following commands:

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
  <li>Common branches
    <ul>
      <li><strong>document</strong><br />Main branch that holds whole content of Clova developer guide. Working branches are forked from this branch and after job is done the branches are merged back to this branch.</li>
      <li><strong>master</strong> (document -> master)<br />Backup branch for <strong>document</strong> branch</li>
      <li><strong>gh-pages</strong> (All lang., Online doc)<br />Web content for internal use (http://pages.oss.navercorp.com/JTF-P6/platform_technical_doc).</li>
    </ul>
  </li>
  <li>Branches for Japan business
    <ul>
      <li><strong>doc-JP</strong> (EN, document -> doc-JP)<br />Branch for Japanese business, this branch holds EN version documentation. JA version will be added future.</li>
      <li><strong>doc-JP-ClovaHomeExt-Partner</strong> (EN, PDF doc, doc-JP -> doc-JP-ClovaHomeExt-Partner)<br />Branch for Japanese partners who provides IoT services via Clova.</li>
      <li><strong>doc-JP-CustomExt-Partner</strong> (EN, PDF doc, doc-JP -> doc-JP-CustomExt-Partner)<br />Branch for Japanese partners who provides extensions via Clova.</li>
    </ul>
  </li>
  <li>Branches for Korean business
    <ul>
      <li><strong>doc-KR</strong> (KO and EN, documnt -> doc-KR)<br />Branch for Korean business, this branch holds KO and EN version documentation.</li>
      <li><strong>doc-KR-En_Partner</strong> (EN, PDF doc, doc-KR -> doc-KR-En_Partner)<br />Branch for Korean partners who prefer English such as Xaomi.</li>
      <li><strong>doc-KR-Partner-LGUplus</strong> (KO, TV STB exclusive spec., PDF doc, doc-KR -> doc-KR-Partner-LGUplus)<br />Branch for LG Uplus (Korean partner) contains LG Uplus exclusive specification.</li>
      <li><strong>doc-KR-Partner</strong> (KO, PDF doc, doc-KR-Partner-LGUplus -> doc-KR-Partner)<br />Branch for Korean partners contains partner exclusive specification.</li>
      <li><strong>doc-KR-Public</strong> (KO, Online doc, doc-KR-Partner -> doc-KR-Public)<br />Branch for public documentation which is deployed on NAVER developer center.</li>
    </ul>
  </li>
</ul>

<a name="Releases" />

## Releases

The release history of Clova developer guide is recorded as GitHub issuse and release feature as below:

* [Issues with Deployment label](https://oss.navercorp.com/JTF-P6/platform_technical_doc/issues?utf8=%E2%9C%93&q=is%3Aissue%20label%3ADeployment%20)
* [Releases](https://oss.navercorp.com/JTF-P6/platform_technical_doc/releases)

> Due to the translation job, EN version documentation is released 1 or 2 week(s) later after KO version release.
