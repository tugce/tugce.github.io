---
layout: post
title:  "Codecademy Günlükleri: AngularJS (1)"
date:   2015-10-04 01:00:00
categories: codecademy angularjs angular salesforce
---
Merhaba,

Bu bir yazı dizisi olacak ve ilk yazım. Codecademy'de AngularJS öğreniyorum ve bunu ilerde Salesforce ile bağlayacağım. İşin ucu mobile bile bağlanabilir. Bakalım, fingers crossed! 

<b>Uyarı:</b> Codecademy de öğrendiğim sırayla anlatıyorum, daha fazla detay için İngilizceniz iyiyse oradaki kursu tavsiye ederim.

Öncelikle AngularJS nedir? Yenir mi? Ona bir bakalım. Üzülerek söylüyorum ki AngularJS yenmiyor. Evet. Bu lanet yenmeyen şey bir javascript frameworkü ve web uygulamalarını kolayca yapmayı ve kontrol etmeyi sağlar. (mış, öyle dediler bana.)

Standart bir AngularJS dizini şöyle bir şey

->css/ <br>
->img/ <br>
->js/ <br>
 -->controllers/ <br>
 -->shared/ <br>
 -->app.js <br>
->index.html <br>

Bir AngularJS uygulaması oluştururken standart akış ise şöyle.

1. app.js içinde bir modül oluştur ve ng-app direktifi ile uygulamanın scope unu belirle

app.js içinde 
{% highlight javascript %}
var app = angular.module("myApp", []);
{% endhighlight %}

index.html içinde
{% highlight html %}
<body ng-app="myApp"></body>
{% endhighlight %}
2.controllers klasörü içinde controller oluştur ve ng-controller direktifi ile controllerın scope unu belirle

js/controllers içinde

MainController.js
{% highlight javascript %}
app.controller('MainController', ['$scope', function($scope){
  $scope.title = 'Salesforce Test';
  $scope.promo = 'Promo Degiskeni';
}]);
{% endhighlight %}
index.html
{% highlight html %}
<div class="main" ng-controller="MainController">
</div> <!-- main -->
{% endhighlight %}
3.controllerda scope değişkenine veri ekle ve bu veriyi expressionlar ile sayfada göster

scope değişkenine veri ekleme bir üstte var onu sayfada gösterme şekli ise şöyle

index.html
{% highlight html %}
<h4>{{ title }}</h4> <!-- bu Salesforce Test  yazacak sayfaya--> 
{% endhighlight %}
Bir obje oluşturmak için 
{% highlight html %}
$scope.objeadı = {field1: "deneme", field2 = 23};
<h4>{{ objeadı.field1 }}</h4> <!-- bu deneme yazısını gösteriyor -->
{% endhighlight %}
AngularJS de filtreler var. (Bu bile yenmiyor. Pes!) Mesela integer sayıyı para birimi olarak göstermek için;
{% highlight html %}
{{ objeadı.field2 \| currency }}
{% endhighlight %}
Angular filtreleri şu şekilde çalışıyor.

1. objeadı.field2 deki değeri alıyor. <br>
2. Sayıyı currency filtresine gönderiyor. Pipe sembolü ( \| )Linux konsol kullanan arkadaşların aşina olduğu bir şey. Görevi aynısı inputu alıp diğer tarafa gönderiyor. <br>
3. Filtre dolar işaretini ve uygun ondalıklı kısmı yerleştiriyor. <br>

Daha fazla filtre için şuraya bakabilirsiniz: <a href="https://docs.angularjs.org/api/ng/filter">Filtreler</a>

Şimdi neler öğrendik?

Modül (app.js de tanımladığımız) Angular uygulamasının farklı bileşenlerini içerir <br>
Controller uygulamanın verilerini yönetir <br>
Expression sayfada verileri göstermeyi sağlar <br>
Filtre expressiondan gelen değerin formatını (biçimini) düzeltir. <br>