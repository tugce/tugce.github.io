---
layout: post
title:  "(Neredeyse) Bir Saat Süren Hata"
date:   2015-10-10 20:00:00
categories: angularjs angular bootstrap npm http-server bug bugfix coding
---

Ha ha ha.

Size çok komik bir olaydan bahsedeceğim. Neredeyse bir saatimi alan bir sorun. Sorun şu. AngularJS ve bootstrap üzerinde çalışıyorum. (Çok çalışkan bir insanımdır ayıptır söylemesi) http-server ile est ediyorum ya bir türlü angularjs controllerdan veri gelmiyor. Lan n'oluyor falan diyorum onu siliyorum bunu ekliyorum olmuyor. Önemli bir şeyi unutmuşum onu ekliyorum nafile. En son çalıştırdığım en basit uygulamaya gidiyorum onu çalıştırayım bakalım diyorum ne göreyim. Çalışmayan uygulama açılıyor. http-server kafayı yedi falan derken jeton paraşütle inmeye başlıyor. Diyorum ki ulan bu bunu belleğe attı sürekli aynı şeyi....LAĞĞĞĞĞĞN. Evet http-server -o ile çalıştırdığım şey 3600 saniye boyunca cache dediğimiz şeyde kalıyormuş. Bu sebeple ben değişiklikleri aslında göremiyormuşum falan. Az daha sabretsem cacheleme süresi bitecekti. onu düzeltmek için

http-server -o -c10

sorunu çözdü. c-c10 10 saniye cachle diyor. Bu da bugünlük bir anımdır.
