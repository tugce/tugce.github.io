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

