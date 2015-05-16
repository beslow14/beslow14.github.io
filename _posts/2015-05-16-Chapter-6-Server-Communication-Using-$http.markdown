---
layout : post
title: "Angular JS 스터디 : 6장 Server Communication Using $http"
categories: angularjs study
---
>>5장에서는 AngularJS 서비스가 컨트롤러와 어떻게 다른지를 살펴보았다.
>>이번장에서는 $http 서비스를 사용해서 서버와 어떻게 통신하는지를 살펴본다.

## $http 로 GET을 사용하여 데이타 가져오기
>>아래는 javascript API를 이용하는 고전적인 방법
{% highlight javascript %}
var xmlhttp = new XMLHttpRequest();

xmlhttp.onreadystatechange = function(){
  if(xmlhttpreadystate == 4 && xmlhttp.status ==200){
    var response = xmlhttp.responseText;
  } else if(xmlhttp.status == 400) {
    //handle error
  }
};
xmlhttp.open("GET", "http://myserver/api",true);
xmlhttp.send();
{% endhighlight %}

>> 이런 방식은 반복적으로 해야 할 게 많기 때문에, Wrapper나 library를 보통 많이 이용하게 된다.
$http는 core AngularJS 서비스로 서버와 endpoint간에 XHR을 사용한 통신을 하도록 해준다.
그러나 XHR은 비동기이기 때문에,, promise interface를 이용하여 이벤트 콜백함수를 처리한다.

#### RESTFUL API
우리의 가상 서버는 아래와 같은 API를 제공해 준다.
- GET /api/note/ => array of note 를 제공
- GET /api/note/:id => 특정 id의 note를 제공
- POST /api/note => 신규 article을 생성
- POST /api/note/:id => id의 article을 업데이트

{% highlight javascript %}
<script>
  angular.module('notesApp',[])
    .controller('MainCtrl',['$http', function($http){
      var self = this;
      self.items = [];
      $http.get('/api/note').then(function(response){
        self.items = response.data;
      }, function(errResponse) {
        console.error('Error while fetching notes');
      });
    }]);
</script>
{% endhighlight %}

>> $http.get()함수는 promise object를 리턴한다.
- then() 함수는 success handler와 error handler 의 두 개를 전달인자로 가진다.
- 서버가 200 ok 응답을 보내주면 success를, 그 외의 응답이 오면 error 핸들러를 부른다.

#### A Deep Dive into Promises
>> Promise의 개념에 대해서 간단하게 살펴본다. AngularJS의 Promise는 Kris Kowal's Q proposal에 기반을 두고 있다. 

>> 요건 전통적인 콜백 반복 호출 방식
{% highlight javascript %}
xhrGet('/api/server-config',function(config){
  xhrGet('/api/'+config.USER_END_POINT, function(user){
    xhrGet('/api/'+user.id+'/items', function(items){
      // Actually display the items here
    });
  });
});
{% endhighlight %}

>> 요건 promise를 용한 호출 방식
{% highlight javascript %}
$http.get('/api/server-config')
.then(function(configResponse){})
.then(function(userResponse){})
.then(
  function(itemResponse){}, 
  function(error){}
);
{% endhighlight %}

#### Propagating Success and Error
>> promise 체이닝은 매무 파워풀한 테크닉이지만, 이것을 사용할 때 꼭 알아 두어야 할 것들이 있다.
{% highlight javascript %}

{% endhighlight %}
