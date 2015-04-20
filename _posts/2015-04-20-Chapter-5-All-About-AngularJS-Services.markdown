---
layout : post
title: "Angular JS 스터디 : 5장 All About AngularJS Services"
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

## 내장된 서비스 사용하기

#### 몇가지 주의할 사항
- 내장된 서비스들은 $ 로 시작한다.
- 서비스를 사용하기 전에 서비스를 inject를 해야한다.
- 아래 예제처럼 배열형태로 사용하는데, 사실 생략도 가능하다. 다만, 생략하게 되면 여러개의 Javascript파일을 하나로 합친다던지 할때, 옵티마이제이션의 결과로 함수의 인자의 이름이 바뀌게 될 것이고, 이 경우 AngularJS 프레임웤이 알수가 없게 된다.
{% highlight javascript %}
<script>
  angular.module('notesApp',[])
    .controller('MainCtrl',['$log',function($log){
      var self = this;
      self.logStuff = function() {
        $log.log('The button was pressed');
      };
    }])
</script>
{% endhighlight %}
- 의존성 주입은 순서가 중요하다.
{% highlight javascript %}
  myModule.controller("MainCtrl", ["$log","$window", function($l,$w){}]);
{% endhighlight %}

## 일반적인 AngularJS 서비스들
$window : window object를 wrapping하는 서비스
$location : 브라우저의 URL입력창과 상호작용하는 서비스(absUrl, url, path, search 같은 함수를 가짐)
$http : AJAX 통신을 하는 서비스이다.

## Angular 서비스 만들기
> 재사용 가능하고, 어플리케이션 레벨이고, 뷰와는 독립적이고, 서드파티 서비스와 결합이 가능하고, Object Caching을 가능케 하는 서비스를 만들 수 있다.

{% highlight javascript %}
  angular.module('noteApp',[])
  .controller('MainCtrl',[function(){
    var self = this;
    self.tab = 'first';
    self.open = function(tab) {
      self.tab = tab;
    };
  }])
  .controller('SubCtrl',['ItemService',
    function(ItemService) {
      var self = this;
      self.list = function() {
        return ItemService.list();
      };
      self.add = function() {
        ItemService.add({
          id: self.list().length + 1,
          label: 'Item ' + self.list().length
          });
      };
    };
  }])
  .factory('ItemService', [function(){
    var items = [
      {id:1, label:'Item 0'},
      {id:2, label:'Item 1'}
    ];
    return {
      list: function() {
        return items;
      },
      add: function(item){
        items.push(item);
      }
    };
  }]);
{% endhighlight %}


## Factory, Service, Provider의 차이점
> 사실 개인적으로 궁금해서 찾아봤었는데, 명쾌하게 이해하기가 어려웠었다. 이 책을 보고 서야 알수가 있었다.

#### Factory
- 함수 스타일의 언어에서 사용된다.
- 함수나 객체를 리턴하는 방식이다.

#### Service
- 앞의 Factory와 크게 차이가 없다.
- 단지, service라는 키워드를 사용하고, 자바스크립트 오리지널 function()을 사용하고(클래스처럼), 객체를 리턴하지 않는 것이 차이점이다.
{% highlight javascript %}
  
  function ItemService(){
    var items = [
      {id:1, label:'Item 0'},
      {id:2, label:'Item 1'}
    ];
    this.list = function() {
      return items;
    };
    this.add = function(item){
      items.push(item);
    };
  }
  
  angular.module('noteApp',[])
  .service('ItemService', [ItemService]);
  .controller('MainCtrl',[function(){
    var self = this;
    self.tab = 'first';
    self.open = function(tab) {
      self.tab = tab;
    };
  }])
  .controller('SubCtrl',['ItemService',
    function(ItemService) {
      var self = this;
      self.list = function() {
        return ItemService.list();
      };
      self.add = function() {
        ItemService.add({
          id: self.list().length + 1,
          label: 'Item ' + self.list().length
          });
      };
    };
  }])
  
  
  
{% endhighlight %}
