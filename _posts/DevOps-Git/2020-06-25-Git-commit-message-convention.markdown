---
layout: post
title: "[Git] Commit Message Convention"
date: 2020-06-25
categories: [DevOps/Git]
author : "Junny"
tags : [Git,commitMessageConvention]
---
# Commit Message Convention
- Commit 메세지 내용에 대한 고민을 하다가 웹사이트에 잘 정리된 내용을 보고 번역하려고한다.<br>
원본 사이트 : [Udacity Git Commit Message Style Guide](https://udacity.github.io/git-styleguide/)

## 소개
- 이 스타일 가이드는 당신의 프로젝트에서 공식적인 가이드 역할은 한다. Udacity 평가자는 당신의 프로젝트를 평가하는데 이 가이드를 사용할 것이다. 개발의 세계에서 "이상적인" 스타일에 대한 많은 의견이 있다. 그러므로 학생들이 프로젝트 과정에서 따라야 할 스타일에 대한 혼동을 줄이려면 모든 학생들이 자신의 프로젝트에 대해 이 스타일 가이드를 참조 할 것을 추천한다.

## Commit Message Structure
- 기본적으로 커밋 메시지는 공백 라인을 가지고 3가지의 분리되어 구성된다 : 제목/본문/꼬리말로 구성된다. 레이아웃은 아래와 같다
<br>

```
type : subject

body

footer
```

<br>
제목은 메세지의 유형과 제목으로 구성된다
## Commit Type
유형은 제목 안에 포함되며 아래의 유형들 중에 하나가 될 수있다.
- feat : 새로운 기능 추가
- fix : 버그 수정
- docs : 문서 수정
- style : 코드 포맷팅, 세미콜론 누락, 코드 변경이 없는 경우
- refactor : 코드 리팩토링
- test : 테스트 코드, 리펙토링 테스트 코드 추가
- chore : 빌드 업무 수정, 패키지 매니저 수정

## Subject
- 제목은 50자를 넘기지 않고, 첫번째는 대문자로 작성하고 마침표를 붙이지 않는다.
- 과거시제를 사용하지 않고 명령조로 작성한다.

## Body
- 선택사항이므로 모든 커밋에대해 설명할 필요는 없다. Body에는 부연설명이 필요하거나 커밋의 이유를 작성한다.
- 72자를 넘기지 않고, 제목과 구분선을 한칸 띄워서 작성한다.
(추가 : 한칸을 띄우는 이유는 git log --oneline 명령어를 사용하면 제목만 나타나기 때문)

## footer
- 선택사항
- issue tracker id를 작성할때 사용한다. #123

## Example Commit Message
<br>

```
feat: Summarize changes in around 50 characters or less

More detailed explanatory text, if necessary. Wrap it to about 72
characters or so. In some contexts, the first line is treated as the
subject of the commit and the rest of the text as the body. The
blank line separating the summary from the body is critical (unless
you omit the body entirely); various tools like `log`, `shortlog`
and `rebase` can get confused if you run the two together.

Explain the problem that this commit is solving. Focus on why you
are making this change as opposed to how (the code explains that).
Are there side effects or other unintuitive consequenses of this
change? Here's the place to explain them.

Further paragraphs come after blank lines.

 - Bullet points are okay, too

 - Typically a hyphen or asterisk is used for the bullet, preceded
   by a single space, with blank lines in between, but conventions
   vary here

If you use an issue tracker, put references to them at the bottom,
like this:

Resolves: #123
See also: #456, #789
```

<br>