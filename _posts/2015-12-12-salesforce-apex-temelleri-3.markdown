---
layout: post
title:  "Salesforce Apex Temelleri - Salesforce (3)"
date:   2015-12-12 23:00:00
comments: true
categories: salesforce apex
---

Bugün Apex'in temellerini anlatacağım. Apex Salesforce'da kullanılan Java benzeri bir programlama dilidir. Sistem olaylarına business logic eklenmesini sağlar. Bunlar butona basma, insert/update edilen kayıtlarla ilgili olylar ya da Visualforce sayfaları olabilir. Apex Force.com platformunda yani sunucu tarafında kaydedilir, derlenir ve çalıştırılır. NEsneye yöneliktir ve veritabanı ile birleşik bir yapısı vardır. Java'ya benzediği için Java bilen birisi için kullanımı çok kolaydır. Hatta bazen dikkatli bir şekilde yazıldığında kodlar Java platformunda bile çalışabilir. Bunun örneğini ilerde vereceğim. Ama şimdi konumuza devam edelim.

Apex'te yeni bir liste tanımlamak istersek bunu şu şekilde yapabiliriz.

{% highlight java %}
List<String> stringListe = new List<String>();
stringListe.add('liste elemanı 1');
{% endhighlight %}

Görüldüğü gibi dil Java'ya bu açıdan çok benziyor. Yazması oldukça kolay hatta benim açımdan eğlenceli bile diyebilirim. Salesforce'a bir kere alıştıktan sonra yazması çok keyifli bir dil. Faka Salesforce kısıtlamalarından dolayı zaman zaman gereğinden fazla uzun kodlar yazmak zorunda kalabiliyor ve yer yer çileden çıkabiliyorum. Yine de I love Salesforce! :)

Apexte for yapısı aşağıdaki gibi.

{% highlight java %}
for(Integer i = 0; i < stringListe.size(); i++){
	system.debug(stringListe[i]);
}
{% endhighlight %}

Görüldüğü gibi oldukça Java benzeri(aynısı) bir yapı var. Apex'te iki farklı koleksiyon tipi daha var. Biri Set diğeri ise Map. İşe ilk başladığımda Apex öğrenirken Map kullanmamak konusunda direniyordum ve Mustafa öğrendikten sonra çok seveceğimi söyleyip duruyordu. Haklıymış, Map gerçekten harika bir yapı. Özellikle birden fazla nesneyi birbirine bağlayarak iş yapmanız gerekiyorsa gereksiz for yapılarından kurtuluyorsunuz. Basit bir Map tanıtımı aşağıdaki gibi.

{% highlight java %}
Map<String, String> stringMap = new Map<String, String>();
stringMap.put('anahtar', 'değer');
system.debug(stringMap.get('anahtar')); //bu loglara değer ifadesini yazacaktır.
{% endhighlight %}

Apex'te temel veri tipleri bulunmaklar beraber hem sistemde tanımlı nesneleri hem de sınıf olarak tanımlayacağınız nesneleri veri tipi olarak kullanabiliyorsunuz.

Bugünlük Apex bu kadar. Bu konuyu daha detaylı olarak sonra anlatmaya devam edeceğim.


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
