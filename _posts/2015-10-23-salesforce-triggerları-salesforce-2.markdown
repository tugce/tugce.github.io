---
layout: post
title:  "Salesforce Triggerları - Salesforce (2)"
date:   2015-10-23 20:00:00
comments: true
categories: salesforce apex trigger
---

Bugün Apex trigger yazımını anlatacağım. Trigger nedir ne değildir onunla başlayalım önce. Salesforce'da insert, update ve delete işlemlerinin öncesinde ve sonrasında (before/after) istenen işlemleri yapabilmek için yazdığımız yapıya trigger diyoruz.

Diyelim ki Account nesnemiz insert edilirken (before) eğer Name alanı 'Tuğçe' ye eşitse Test__c alanımızda da Tuğçe yazsın. Burada akışımız şu şekilde ilerliyor. Account tipinde a kaydı insert işlemi başlar --> Name == Tuğçe koşulu kontrol edilir --> Eğer doğruysa a.Test__c = a.Name yapılır.

Dikkat ettiyseniz burada tekrar bir update işlemi uygulamadık. Çünkü before triggerlarında henüz veritabanına kayıt kaydedilmediği için update etmemize gerek kalmadı. Zaten Triggerın içeriğinde olan nesneler before triggerlarında insert/update ya da delete edilemezler.

Triggerlar Salesforce'da tıklama ile yapılamayacak durumlarda kullanılmalıdır. (Salesforce'taki tıklama yapıları sonraki yazılarımdan birilerinde olacaktır.) Triggerları isteğe göre aktif ya da inaktif yapabiliriz. Ayrıca production dediğimiz canlı ortama taşınacak trigger kodları %1 bile olsa code coverage dediğimiz testlere sahip olmalıdır. Salesforce'da unit testleri <a href="http://ztugcesirin.com/salesforce/apex/unittests/test/2015/10/22/salesforce-unit-testler/">burada</a> anlatmıştım.

Basit bir trigger yazalım şimdi.

{% highlight java %}
trigger UpdateTest on Account (before insert) {
    List<Account> accounts = Trigger.new; //yeni insert edilen Account nesneleri

    For(Account a :accounts){
      if(a.Name == 'Tuğçe') a.Test__c = a.Name;
    }
}
{% endhighlight %}

Yukarda bahsettiğimiz akışın algoritması bu şekilde yazılıyor. Şimdi burada Trigger.new dedik. Bu Trigger.new yeni insert edilen Account tipindeki kayıtları getiriyor.

Trigger.new - > yeni kayıtlar <br>
Trigger.old - > update/delete edilmeden önceki halleri <br>
Trigger.newMap - > yeni kayıtların idleri ile map edilmiş halleri <br>
Trigger.oldMap - > update/delete edilmeden önceki kayıtların idleri ile map edilmiş halleri

Bunlar bizim kodda toplu halde işlem yapabilmemizi kolaylaştırır. Salesforce'ta çok fazla limit olduğu için bu limitlere çok yaklaşmamızı da sağlar.

Diyelim ki triggerımız before insert ve after update durumları için geçerli olsun. Bu insert ve delete , before ve after durumları için kodu nasıl ayıracağız?

{% highlight java %}
trigger UpdateTest on Account (before insert, before update) {
  if(Trigger.isBefore){
    List<Account> accounts = Trigger.new; //yeni insert edilen Account nesneleri

    For(Account a :accounts){
      if(a.Name == 'Tuğçe') a.Test__c = a.Name;
    }
  }else if(Trigger.isAfter){
    //after kodu
  }
}
{% endhighlight %}
ya da

{% highlight java %}
trigger UpdateTest on Account (before insert, before update) {
  if(Trigger.isInsert){
    List<Account> accounts = Trigger.new; //yeni insert edilen Account nesneleri

    For(Account a :accounts){
      if(a.Name == 'Tuğçe') a.Test__c = a.Name;
    }
  }else if(Trigger.isUpdate){
    //update kodu
  }
}
{% endhighlight %}

isInsert, isUpdate, isDelete, isBefore, isAfter bizim tek bir triggerda farklı koşullar için işlemler yapabilmemizi sağlar. Salesforce'ta trigger yazımı kısa böyle. Daha detaylı öğrenmek isteyen arkadaşları <a href="https://developer.salesforce.com/trailhead">Trailhead</a> e davet ediyorum. Trailhead, aynı Codecademy gibi adım adım ilerleyerek öğrenmeyi sağlayan bir araç. (Codecademy ne diye sormayın n'olursunuz...) İlgileniyorsanız bakmanızı tavsiye ederim.
<div id="disqus_thread"></div>
<script>
    /**
     *  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
     *  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables
     */
    /*
    var disqus_config = function () {
        this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
        this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
    };
    */
    (function() {  // DON'T EDIT BELOW THIS LINE
        var d = document, s = d.createElement('script');

        s.src = '//ztugcesirincom.disqus.com/embed.js';

        s.setAttribute('data-timestamp', +new Date());
        (d.head || d.body).appendChild(s);
    })();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript" rel="nofollow">comments powered by Disqus.</a></noscript>
