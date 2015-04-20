---
layout : post
title: "Angular JS 스터디 : 4장 All About AngularJS Services"
categories: angularjs study
---
> 지금까지는 AngularJS의 데이타 바인딩에 대해서 알아보았다. (UI<->Controller 의 바인딩,)
> 이 장에서는 AngularJS의 서비스에 대해 알아본다

## AngularJS Servies란
> 동작이나 상태를 가지고 있는 함수나 객체이다.

## Services vs. Controllers
> Controller가 UI나 Presentation logic을 맡는다면, Service는 Business logic이나 재사용가능하고 어플리케이션의 전역적인 역할을 맡는다.

## Dependency Injection
> 우리가 서비스 인스턴스를 만드는게 아니라 인젝터라고 부르는 함수나 클래스가 대신 객체를 생성해서 넘겨주는 것이다.

{% highlight javascript %}
// Without Dependency Injection
function fetchDashboardData(){
  var $http = new HttpService();
  return $http.get('my/url');
}

// With Dependency Injection
function fetchDashboardData($http) {
  return $http.get('my/url');
}
{% endhighlight %}

