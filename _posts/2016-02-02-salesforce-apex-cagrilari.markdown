---
layout: post
title:  "Salesforce Apex Çağrıları (5)"
date:   2016-02-02 20:00:00
categories: salesforce apex programming
---

Merhabalar,

Bugün bazılarınızın şaşırabileceği bir şekilde yine ve yeniden Salesforce ve Apex'ten bahsedeceğim size. Bugünün konusu ise Apex çağrıları. Bu çağrılar nelerdir önce onlardan kısaca bahsedeyim.

Bir Apex çağrısı Apex kodunuzu dışardaki bir servisle bağlamanızı sağlar. Çağrı Apex kodundan dışardaki web servise çağrı yapar ya da HTTP isteği gönderir ve karşılık olarak bir response alır. Bu iki şekilde olabilir.

1. XML kullanan SOAP çağrıları. Genelde kod oluşturmak için bir WSDL belgesine ihtiyaç duyar. </br>
2. Genelde JSON kullanan REST HTTP istekleri </br>

Bunlar servise istek yapma ve yanıt alma konusunda birbirine benzese bile WSDL tabanlı çağrılar SOAP web servisleriyken HTTP çağrıları SOAP ya da REST kullanan herhangi bir HTTP servisi olabilir.

Salesforce'da çağrı yapabilmek için öncelikle çağrı yapılacak adresi (endpoint) Remote Site Settings'e eklemek gerekir. Bu örneğimiz için benim yazdığım çok basit bir servisi kullanacağım. Remote Site Settings'e aşağıdaki şekilde http://sleepy-fortress-56786.herokuapp.com adresini ekleyelim.

Setup - > Quick Find kutusu -> Remote Site Settings -> New -> İsim ve URL alanları doldurulacak - > Save

Şimdi Developer Console'u açalım ve web servisimizi test edelim. Bu yazımda sadece HTTP isteklerinin örneğini yapacağım. Ama SOAP için örnek görmek isteyenler Trailhead'den bakabilir. Developer Console -> Debug -> Open Execute Anonymus Window u açalım ve aşağıdaki kodu alana kopyalayıp Execute butonuna basalım. Ekrana gelecek olan logda Debug Only seçeneğini seçtiğimizde Hello: Hello World yazısını JSON formatında görebilirsiniz.

{% highlight java %}
Http http = new Http();
HttpRequest request = new HttpRequest();
request.setEndpoint('http://sleepy-fortress-56786.herokuapp.com/v1/api/hello');
request.setMethod('GET');
HttpResponse response = http.send(request);
if (response.getStatusCode() == 200) {
    System.debug(response.getBody());
}
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
