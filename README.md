## 소개
이 저장소는 [NAVER 개발자 센터](https://developers.naver.com/main/)에 [Clova 개발자 가이드](https://developers.naver.com/docs/clova/guide/) 문서를 배포하기 위해 생성되었습니다.

문서에 대한 피드백은 [NAVER 개발자 센터 포럼](http://forum.developers.naver.com/)을 이용하거나 이 저장소에 대한 [이슈](https://github.com/naver/clova-developer-guide/issues)를 등록해주시면 됩니다.

기술 문서에 대한 문의나 자세한 사항은 [jeongil.kang@linecorp.com](mailto://jeongil.kang@linecorp.com)로 연락바랍니다.

## 저작권

ⓒ NAVER Corp. All Rights Reserved.

이 문서는 NAVER㈜의 지적 자산이므로 NAVER㈜의 승인 없이 이 문서를 다른 용도로 임의 변경하여 사용할 수 없습니다.
이 문서는 정보제공의 목적으로만 제공됩니다. NAVER㈜는 이 문서에 수록된 정보의 완전성과 정확성을 검증하기 위해 노력하였으나, 발생할 수 있는 내용상의 오류나 누락에 대해서는 책임지지 않습니다. 따라서 이 문서의 사용이나 사용 결과에 따른 책임은 전적으로 사용자에게 있으며, NAVER㈜는 이에 대해 명시적 혹은 묵시적으로 어떠한 보증도 하지 않습니다. 관련 URL 정보를 포함하여 이 문서에서 언급한 특정 소프트웨어 상품이나 제품은 해당 소유자의 저작권법을 따르며, 해당 저작권법을 준수하는 것은 사용자의 책임입니다.

<<<<<<< HEAD
NAVER㈜는 이 문서의 내용을 예고 없이 변경할 수 있습니다.
=======
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
>>>>>>> doc-KR-Partner
