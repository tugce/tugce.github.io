---
layout: post
title:  "Tomcat ClassNotFound Hatası"
date:   2015-12-13 18:45:00
comments: true
categories: tomcat eclipse spring
---

Geçenlerde çok başımı ağrıtan bir sorun vardı. Şimdi iki proje düşünelim. Proje 1 ve Proje 2. Proje 2, Proje 1'e bağımlı olsun. Eclipse'de Proje 2'yi tomcat üzerinde çalıştırmaya çalıştığımda sürekli Proje 1'e ait bir sınıf bulunamadı hatası alıyordum. Ama şöyle bir durum vardı ki Proje 2 dependency hatası vermiyordu. Yani her şey yolunda olmalıydı. Öyle miydi? Sorunu internette çok arattım ama tam olmuyor bulamıyorum diye ağlamaya başlayacakken... Evet doğru bildiniz. Stackoverflow'da bir yanıt gördüm. Çok çok mantıklı görünüyordu. Test ettim ve sorun çözüldü. Sorunun nasıl mı çözülüyor? Öncelikle şu <a href="http://stackoverflow.com/questions/5603758/tomcat-throws-classnotfound-exceptions-for-classes-in-other-open-eclipse-project">süper</a> yanıtın orijinalini koyayım buraya.

Sorunun sebebi Tomcat yapılandırmasında Proje 1'in dizin yolunun bulunmamasıymış. Çözmek için;


1. Eclipse'de Window - > Show View - > Servers - > Servers'ı açalım.<br>
2. Servers'da yapılandırmak istediğimiz serverın üzerine çift tıklayalım. (Benim durumumda Tomcat 8)<br>
3. Bu Overview isminde bir pencere açmış olmalı.<br>
4. Bu pencerede Open launch configuration linkini bulun ve bu linke tıklayın.<br>
5. Classpath sekmesini açın.<br>
6. User Entries satırına tıklayın.<br>
7. Kenardaki Add Projects butonuna basın.<br>
8. Sunucunun bulmasını istediğiniz projeyi seçin.<br>
9. Önce Apply butonuna sonrasında ise OK butonuna basın.<br>
10. Sunucuyu tekrar başlatın.<br>

İşte bu kadar. ClassNotFound hatasına elveda deyin ve projenizin çalışmasının tadını çıkarın. Tabi başka sevimli hatalar ortaya çıkmazsa... :)


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
