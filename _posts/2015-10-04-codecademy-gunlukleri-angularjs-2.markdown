---
layout: post
title:  "Codecademy Günlükleri: AngularJS (2)"
date:   2015-10-04 10:00:00
categories: codecademy angularjs angular salesforce
---
Merhaba,

Geçen <a href="http://ztugcesirin.com/codecademy/angularjs/angular/salesforce/2015/10/04/codecademy-gunlukleri-angularjs-1"/>yazımda</a>AngularJS ye bir giriş yapmıştım. Şimdi devam edelim. En son verileri sayfada gösterebiliyorduk. Diyelim birden fazla veriyi göstermemiz gerekti. Onu nasıl yapacağız? Şöyle ki;

MainController.js
{% highlight javascript %}
$scope.listeadı= [ 
  { 
    alan1: 'deneme', 
    alan2: 19, 
    alan3: 'test'
  }, 
  { 
    alan1: 'angularjs', 
    alan2 42, 
    alan 3: 'ogren'
  } 
];
{% endhighlight %}
index.html
{% highlight html %}
<div ng-repeat="lst in listeadı" class="test"> 
  <div class="thumbnail"> 
    <p class="t1">{{ lst.alan1}}</p> 
    <p class="t2">{{ lst.alan2 }}</p> 
    <p class="t3">{{ lst.alan3 }}</p> 
  </div> 
</div>
{% endhighlight %}
Burada gördüğünüz gibi ng-repeat kullanıyoruz. ng-repeat te ng-app ve ng-controller gibi bir directive. Direktifler HTML elemanlarının davranışını belirler. Uygulama çalıştığında AngularJS bu özelliği trigger eder.

Şimdiye kadar statik bir AngularJS uygulaması yaptık. Şimdi biraz interaktif özellikler ekleyelim.

Şimdi beğeni olarak bir özellik ekleyelim.

index.html

{% highlight html %}
<div class="reputation"> 
      <p class="rep" ng-click="arttir($index)"> {{ kisi.rep }} + </p> 
    </div>
{% endhighlight %}
MainController.js
{% highlight html %}
$scope.rep = 0;
$scope.arttir = function(index){
  	$scope.kisiler[index].likes+= 1;
  };
{% endhighlight %}
ng-click de bir direktif. p class=likes tıklandığı zaman ng-click AngularJS ye gereken fonksiyonu çalıştırmasını söylüyor.

Sıfırdan bir Angular uygulaması geliştirdik. Tam uygulamayı Github hesabımdan görebilirsiniz. Çok basit bir şey oldu ama ben biraz biraz öğrendim diyebilirim.

Son olarak şunları söyleyebiliriz.

1.Kullanıcı AngularJS uygulamasını ziyaret eder.<br>
2.view uygulamanın verilerini expression, filtre ve direktifler ile gösterir. Direktifler JTML elemanlarının davranışlarını belirler.<br>
3.bir kullanıcı view daki bir elemana tıklarsa AngularJS bir direktif var mı diye bakar varsa onu çalıştırır.<br>
4.Controllerdaki fonksiyon veriyi günceller.<br>
5.view veriyi otomatik olarak değiştir yeni güncellenmiş veriyi hemen gösterir sayfayı tekrar yüklemeye gerek yoktur.<br>

Sonra uygulamayı lokalde çalıştırmak için node.js kurup web-server için npm install http-server -g komutunu kullandım. Sonra uygulamanın dosyası içinde http-server -o dediğimde uygulama çalıştı.

İş bilgisayarım windows olduğu ve internetimi sadece telefonumdan sağlayabildiğim için benim için biraz zorlu bir öğrenim süreci oluyor. İnternette bu tür konularda sorunların çözümleri genelde Linux dağıtımları üzerinden anlatıldığı için karşılaştığım sorunları çözmesi çok vaktimi aldı diyebilirim. En kısa sürede kendi bilgisayarımda çalışmaya devam etmeyi umuyorum.
