---
layout: post
title:  "Zabbix ile Log İzleme"
date:   2016-02-17 10:00:00
categories: zabbix log monitoring 
---

Merhaba,
<i>Zabbix, Alexei Vladishev tarafından geliştirilen ağlar ve uygulamalar için bir kurumsal açık kaynak izleme çözümüdür.</i> diyor wikipedia Zabbix için. Zabbix ile logları izlemek için gereken adımları anlatacağım bugün.

Zabbix ile log dosyalarını izlemek için öncelikle bir itema ihtiyacımız var.

Bunun için monitor ekranımızdan Configuration - > Hosts -> Log dosyasının bulunduğu host -> Items -> Üst sağ köşede bulunan Create Item adımlarını izliyoruz ve aşağıdaki gibi alanları dolduruyoruz.

<img src="http://ztugcesirin.com/assets/zabbix-log1.png"/>

Key kısmında ilk parametre log dosyasının tam yolu diğeri ise log dosyasında izlenmesini istediğimiz kelime yer almalı. Type Zabbix agent (active) olarak seçilmeli ve Type of Information'da Log olmalı. Bunların ardından itemın görünmesini istediğimiz alanı seçip bir açıklama ekleyerek itemı kaydediyoruz. Şimdi bakalım gereken veriyi alabiliyor muyuz?

Monitoring -> Latest Data altında yeni oluşturduğumuz item görünüyor ise sorunumuz yok demektir. Ekledikten sonra itemın latest data içinde görünmesi için biraz beklememiz gerekiyor.

<img src="http://ztugcesirin.com/assets/zabbix-log2.png"/>

Şimdi tamam logu izleyebiliyoruz ama bizim hata durumların haberimiz olsun istiyoruz. Bunun için öncellikle bir triggera sonrada bu trigger sonucunda çalışacak actiona ihtiyacımız var.

Trigger oluşturmak için Configuration - > Hosts -> Log dosyasının bulunduğu host -> Triggers -> Create trigger adımlarını seçiyoruz.

<img src="http://ztugcesirin.com/assets/zabbix-log3.png"/>

Expressionda logdan gelen son datada fail kelimesi geçiyorsa trigger edilsin diyoruz. Önem seviyesini Yüksek seçip kaydediyoruz. Şimdi bu trigger tetiklendiğinde ana sayfada bunu görebiliriz. 

<img src="http://ztugcesirin.com/assets/zabbix-log4.png"/>

Sürekli bu sayfayı gözetleyemeyeceğimiz için bize email atması özelliğini ekleyelim. Bunun için bir actiona ihtiyacımız var. Configuration - > Actions -> Create Action seçeneklerini seçiyoruz.

Burada Action Conditions ve Operations alanlarını doldurmamız gerekiyor. Action işlemin içeriği ile ilgilenirken Conditions işlemin koşullarını belirliyor. (Trigger Name de Log kelimesi geçiyorsa ya da Trigger Severity High ise gibi) Operations ise yapılacak işlemi belirliyor. Email sms gönderimi gibi seçenekler mevcut.

<img src="http://ztugcesirin.com/assets/zabbix-log5.png"/>
<img src="http://ztugcesirin.com/assets/zabbix-log6.png"/>
<img src="http://ztugcesirin.com/assets/zabbix-log7.png"/>

Bunu da kaydettikten sonra logumuzda fail kelimesi geçtiğinde belirlediğimiz kullanıcılara mail gönderilecektir.