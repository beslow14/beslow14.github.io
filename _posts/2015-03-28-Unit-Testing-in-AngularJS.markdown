---
layout : post
title: "Angular JS 스터디 : 3장 Unit Testing in AngularJS"
categories: angularjs study
---

책 스터디 

#Unit Testing은 무엇이고 왜 하는가?

Unit Testing : function이나 코드가 의도한대로 동작하도록 테스팅

보통 서버 단에서는 일반적이나, 클라이언트에서는 일반적이지 않다.

그러나, 클라이언트에서도 Unit Test를 해야할 다섯가지 이유가 있다.

0. 'Proof of correctness' : end-to-end에 대한 맹목적인 믿음이 아닌, 의도한 대로 동작하는지에 대해 증명할 필요가 있음
0. 'Lack of compiler' : 컴파일가 없어 미리 오류 검출이 안되고, 브라우저마다 동작이 제각각이다.
0. 'Catch errors early' : (유닛테스트가 없다면) 브라우저의 Refresh버튼을 누른다음에야 에러를 찾을 수 있다.
0. 'Prevent regressions' : 다른 개발자들이 코드 베이스를 수정했을때 에러 발생을 막을 수 있다.
0. 'Specification' : 코드가 바뀌면, 유닛 테스트가 깨지게 되기 때문에, 코멘트의 업데이트를 강제한다. 결과적으로 이는 살아있는 스펙이 된다.

#Karma 소개

###테스트 러너(Test Runner) vs 테스트 프레임워크(Test Framework)
`테스트 러너` : 코드 베이스에서 유닛 테스트를 찾고, 브라우저를 열고, 브라우저에서 테스트를 돌리고, 결과를 저장함

테스트가 어떤 언어나, 어떤 프레임웍으로 쓰여졌는지는 상관하지 않음.

`테스트 프레임워크` : Test case를 작성할때의 Syntax나 APIs, Assertion 이다. 꼭 Jasmine이 아니라도 되며, mocha나 다른 거라도 상관없다.

####카르마 설치
https://karma-runner.github.io/0.12/intro/installation.html

{% highlight bash %}
# Install Karma:
npm install karma --save-dev

# Install plugins that your project needs:
npm install karma-jasmine karma-chrome-launcher --save-dev

# Run Karma:
# ./node_modules/karma/bin/karma start 하는 것 대신 아래 commandline 툴을 설치 함.
npm install -g karma-cli
{% endhighlight %}

#### 카르마 설정하기
https://karma-runner.github.io/0.12/config/configuration-file.html


#### 카르마 플러그인
앞에서 2가지 플러그인을 npm명령을 통해서 인스톨했다.(chrome 런처와 jasmine 테스트 프레임워크)
카르마 플러그인은 대략 아래 4가지로 구분되어질 수 있다.

- 브라우저 런처
- 테스트 프레임워크
- Repoters
- Integrators


##Karma Config 설명

##Karma Config 생성

#Jasmine: Spec Style of Testing

##Jasmine Syntax

##Useful Jasmine Matchers

#우리가 만든 Controller를 위한 Unit Test 작성하기

#Unit Test 실행하기

#결론
