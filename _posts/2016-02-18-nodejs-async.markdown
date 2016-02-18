---
layout: post
title:  "Node.js Async (5)"
date:   2016-02-18 10:00:00
categories: nodejs JavaScript programming async
---

Merhabalar,
Bugün Node.js'de kullanılabilen async modülünden bahsedeceğim. Async modülü 20 civarı asenkron fonksiyon içeriyor fakat bu yazımda sadece 4 tanesini (series, parallel, forever, waterfall) açıklayıp kod örnekleri ile detaylandırmaya çalışacağım.
<b>series:</b> async.series görevlerin olduğu bir dizide her bir görev kendisinden önce gelen tamamlandıysa çalışır. Eğer serideki herhangi bir fonksiyon callback fonksiyonuna hata (error) dönerse kalan fonksiyonlar çalıştırılmaz. series fonksiyonunu birbirine bağlı <i>olan</i> bir dizi görev varsa ve bu görevler bittikten sonra bir işlem yapılması gerekiyorsa kullanmalıyız.

{% highlight javascript %}
var async = require('async');

var squareOfNumber = function (number, callback) {
    square = number * number;
    console.log(square);
    if (square == 9) callback("error");
    else callback();
    return square;

};

async.series(
    [
        function(callback){
            squareOfNumber(2,callback);
        },function(callback){
            squareOfNumber(3,callback);
        },function(callback) {
            squareOfNumber(4, callback);
        }
    ], function(err){
        if(err){
            console.log(err);
            return err;
        }
    }
);

--Çıktısı--
4
9
error
{% endhighlight %}

<b>parallel:</b> async.parallel fonksiyonunda dizideki görevler bir öncekinin bitmesini beklemeden çalışır. Bütün görevler bittiğinde yanıtlar final callbacke dizi olarak gönderilir. async.parallel fonksiyonunu birbirine bağlı <i>olmayan</i> bir dizi görev varsa ve bu görevler bittikten sonra bir işlem yapılması gerekiyorsa kullanmalıyız.

{% highlight javascript %}
var async = require('async');

var squareOfNumber = function (number, callback) {
    square = number * number;
    console.log(square);
    if (square == 9) callback("error");
    else callback();
    return square;

};

async.parallel(
    [
        function(callback){
            squareOfNumber(2,callback);
        },function(callback){
            squareOfNumber(3,callback);
        },function(callback) {
            squareOfNumber(4, callback);
        }
        ], function(err){
        if(err){
            console.log(err);
            return err;
        }
    }
);

--Çıktısı--
4
9
error
16


{% endhighlight %}

<b>forever:</b> async.forever fonksiyonu asenkron f(n) fonksiyonunu kendisini tekrar çağırmasını sağlayan callback parametresi ile çağırır. Bunu async.series fonksiyonunun sonsuza kadar çalışan hali olarak düşünebiliriz. Eğer callbacke hata gönderilirse çalışma durur.

{% highlight javascript %}

{% endhighlight %}

<b>waterfall:</b> async.waterfall fonksiyonu fonksiyonlardan oluşan bir görev dizisini çalıştırır ve her bir fonksiyon sonucunu dizide bir sonra gelen fonksiyona gönderir. Ama herhangi bir fonksiyon callbackine hata değeri gönderirse sıradaki fonksiyon çağrılmaz ve ana callback hata değeri ile çağrılır. async.waterfall fonksiyonu kendisinden bir önceki fonksiyonun sonucu ile işlemler yapacak işlemler için kullanılır.

{% highlight javascript %}
var async = require('async');

async.waterfall([
    function(callback) {
        console.log("ilk islem yapıldı");
        callback(null, 'dosya');
    },
    function(arg1, callback) {
        console.log(arg1);
        callback(null, 'degisken');
    },
    function(arg1, callback) {
        console.log(arg1);
        callback(null, 'final');
    }
], function (err, result) {
        console.log(result);
});

--Çıktısı--
ilk islem yapıldı
dosya
degisken
final

{% endhighlight %}

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
