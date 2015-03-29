---
layout : post
title: "Angular JS 스터디 : 4장 Forms, Inputs,and Services"
categories: angularjs study
---

기본 제공해주는 서비스에 대해 알아본다.

# Working with ng-model

###one way data binding
model <-> view 사이의 데이타를 바인딩
여기서 model은 controler의 data
view는 html tag내의 ng-bind 또는 {{ }}로 싸여진 부분

###two way data binding
view(forms, Inputs) <-> model <-> view 사이의 데이타를 바인딩
ng-model로 바인딩 됨. 
<input type=”text” ng-model=”ctrl.username” />
you typed {{ctrl.username}}

# Working with Forms
폼을 사용할 때, 코딩을 줄여주는 팁

1. ng-click 대신 ng-submit 사용
    - ng-click : 버튼을 클릭할때만 이벤트가 발생
    - ng-submit : 버튼을 클릭할때나, 엔터 입력할 때도 이벤트 발생함

2. 변수보다는 Object를 사용
ex)변수 : ctrl.username , ctrl.password 말고
     Object : ctrl.user.name , ctrl,user,password를 사용 
     * 명시적으로 this.user = {} 를 선언안해도 AnguralJS에서 추가해 줌.
     

# Leverage Data-Binding and Models
form의 data를 object형태로 모델링 하는 것이 일을 줄일 수 있기 때문에 유리하다.

#Form Validation and States
Form Validation을 위한 directive : ng-minlength, ng-disabled
Form을 사용하게 되면, AngularJS는 FormContorller를 생성(Form State 및 helper method를 가짐) 
  - Form State : $invalid, $valid, $pristine(최초상태), $dirty(초기의 반대), $error

아래는 username을 4자리 밑으로 입력시, submit 버튼을 안보이도록 설정 하는 예제임.
{% highlight javascript %}
<form ng-submit=”ctrl.submit()” name=”myForm”>
  <input type=”text” ng-model=”ctrl.user.username” required ng-minlength=”4”>
  <input type=”password” ng-model=”ctrl.user.password” required >
  <input type=”submit” value=”Submit” ng-disabled=”myForm.$invalid”>
</form>
{% endhighlight %}


# Error Handling with Forms
AngularJS가 제공하는 기본 Validators
-custom validators는 13장에서..

### Display Error Messages

어떻게 에러 내용을 유저에게 잘 전달해 줄수 있을까?
-input state값을 체크해, 에러메시지를 전달(html tag만으로..)

{% highlight javascript %}
<form ng-submit=”ctrl.submit()” name=”myForm”>
 <input type=”text” name=”uname” ng-model=”ctrl.user.username” required ng-minlength=”4”>
  <span ng-show=”myForm.uname.$error.required”>
   this is a required field </span>
  <span ng-show=”myForm.uname.$error.minlength”>
   Minimum length required is 4 </span>
  <span ng-show=”myForm.uname.$invalid”>
    This field is invalid </span>
{% endhighlight %}

### Styling and States
input state 와 css 값을 연결하여, 잘못된 입력이 들어왔을때, 하이라이트가 가능하다.

# Nested Forms with ng-form

HTML form은 subform을 지원하지 않지만, Angular JS는 ng-form directive를 통해서 지원이 가능함.
profile.$invalid 나 myForm.proflie.$invalid 로 접근가능함.
{% highlight javascript %}
<form name=”myForm”>
  <ng-form name=”profile”>
  </ng-form>
</form>
{% endhighlight %}

# Other Form Controls

### TextAreas
input text와 동일

### Checkboxes
<div ng-repeat=”sport in ctrl.sports”>
1.데이타를 바인딩 시킴
<input type=”checkbox” ng-model=”sport.selected” ng-true-value=”YES” ng-false-value=”NO”>
2, 값을 읽어오고, 바인딩 시키지는 않음
<input type=”checkbox” ng-checked=”sport.selected === ‘YES’”>

</div>

<script>
this.sports = [{label:”Basketball”, selected:”YES}, {...}, {...}]
</script>


### Radio Buttons
라디오 버튼은 체크 박스와 거의 동일하나,, 특성상 하나를 선택하면 다른 것들은 해제되어야 함
{% highlight javascript %}
<div ng-init=”user = {gender:’female’}”>
	<input type=”radio” name=”gender” ng-model=”user.gender” value=”male”>
	<input type=”radio” name=”gender” ng-model=”user.gender” value=”female”>
</div>
{% endhighlight %}

### Combo Boxes / Drop Downs
