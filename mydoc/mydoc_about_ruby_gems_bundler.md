---
title: About Ruby, Gems, Bundler, and other prerequisites
tags: [getting_started, troubleshooting]
keywords:
summary: "Ruby is a programming language you must have on your computer in order to build Jekyll locally. Ruby has various gems (or plugins) that provide various functionality. Each Jekyll project usually requires certain gems."
sidebar: mydoc_sidebar
permalink: /mydoc_about_ruby_gems_etc/
---

[TOC]

## 화면 구성 및 운영

### LIVE 화면 구성
WIZEYE 사이트 화면은 크게 RIBBON 영역, LEFT/RIGHT PANEL 영역, VIEW 영역, FOOTER영역으로 구성되어 있다.

화면 구성은 아래 그림과 같다.



![iTerm profile example]({{ "/images/itermexample.png" | prepend: site.baseurl }})

<table id="sampleTable" class="display">
   <thead>
      <tr>
         <th>번호</th>
         <th>설명</th>
         <th>설정 변경 방법</th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td>1</td>
         <td>GRID기능을 이용해 VIEW를 구성한다.</td>
         <td>시작화면에서 Grid를 화면에 표현하는 방식을 설정한다.
UI SETTING → Theme Options → LIVE → Page Setting → GRID Start Settings
</td>
      </tr>
      <tr>
         <td>2</td>
         <td>VIEW영역은 여러 개의 CELL로 구성된다.
VIEW영역은 여러 개의 CELL로 분할하거나 여러 CELL을 하나의 CELL로 병합할 수 있다.
         </td>
         <td></td>
      </tr>
    <tr>
       <td>3</td>
       <td>각 CELL에는 Contents (Map, Camera, Chart)를 올릴 수 있다.
       </td>
       <td></td>
    </tr>
      <tr>
         <td>4</td>
         <td>현재 보고 있는 VIEW를 저장하고, 저장된 VIEW를 볼 수 있다.
         </td>
         <td></td>
      </tr>
   </tbody>
</table>

### RIBBON영역 구성 및 운영

_ _ _

### PANEL영역 구성 및 운영
_ _ _



Bundler looks in a project's "Gemfile" (no file extension) to see which gems are required by the project. The Gemfile lists the source and then any gems, like this:
 
```
사용자 등록
   * 사용자 이름은 영어로 6자 이상이어야 한다.
   * 사용자 ID는 알파벳과 '-' 또는 숫자 조합으로 3자리 이상 이여야 한다.
   * 비밀번호는 영문+숫자로 10자 이상이거나 영문+숫자+특수문자 8자 이상이어야 한다.

```



