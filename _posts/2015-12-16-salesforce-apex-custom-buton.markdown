---
layout: post
title:  "Salesforce Apex ile Custom Buton Oluşturma (4)"
date:   2015-12-16 20:00:00
categories: salesforce apex programming
---

Merhaba Dünya!

Bugün size yine Apex dilinden bahsedeceğim. Aslında bu benimde yeni keşfettiğim bir şey. Daha önce nasıl keşfetmedim bilmiyorum yani o kadar temel bir konu ki aslında ama bilmiyordum işte. Neyse hep birlikte öğrenelim.

Temel olarak yapacağım şey Salesforce'da bir nesneye custom bir buton eklemek. Diyelim ki bir Account kaydı üzerinde butona tıkladığımızda o Account'a ait tüm Opportunity'ler Closed Won aşamasına getirilsin. Şimdi sınıfımızı yazalım.
{% highlight java %}
global class CloseOpps{
    
    webservice static Integer closeWonOpps(String accId){
        List<Opportunity> opps = [SELECT Id, StageName, AccountId FROM Opportunity WHERE AccountId = :accId];

        if(opps.size() > 0){
            For(Opportunity opp : opps){
                opp.StageName= 'Closed Won';
            }
            update opps;
            return 1;
        }else{
            return 0;
        }
    }
}
{% endhighlight %}
Şimdi sınıfımızı hazırladık. Sıra geldi butonu hazırlamaya.

1. Setup'a girin.
2. Yan sekmeden Customize -> Accounts -> Buttons,Links and Actions kısmını seçin ve New Button and Link butonuna tıklayın.
3. Label kısmına Opportunity Closed Won yazın.
4. Display Type için Detail Page Button kısmını seçin.
5. Davranış kısmına Execute Javascript seçin.
6. Content Source için Execute Javascript seçin.

Şu Javascript kodunu text alana yazalım.
{% highlight javascript %}
{!REQUIRESCRIPT("/soap/ajax/29.0/connection.js")}
{!REQUIRESCRIPT("/soap/ajax/29.0/apex.js")}
var sonuc = sforce.apex.execute("CloseOpps","closeWonOpps",{accId:'{!Account.Id}'});
if(sonuc == 1) alert("Bütün opportunityler Closed Won yapıldı!");
else alert("Hiç Opportunity yok.")
window.location.reload();
{% endhighlight %}

Sonrasında bu butonu page layouta eklersek her şey tamamdır. Herhangi bir Account kaydına gidip butona tıkladığımız zaman o Account kaydına bağlı tüm Opportunitylerin Closed Won olduğunu göreceğiz.

<img src="http://ztugcesirin.com/assets/sfss2.PNG"/>
<img src="http://ztugcesirin.com/assets/sfss3.PNG"/>
<img src="http://ztugcesirin.com/assets/sfss1.PNG"/>

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
