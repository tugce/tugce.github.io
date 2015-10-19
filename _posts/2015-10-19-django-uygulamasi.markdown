---
layout: post
title:  "Basit Bir Django Uygulaması (1)"
date:   2015-10-19 22:22:00
categories: python django coding
---

Bu aralar sürekli farklı farklı şeylere bakıyorum. Bugün kendime konu olarak Django'yu seçtim. Ha böyle daldan dala atlamam iyi bir şey mi ondan emin değilim. Ama şu an için bir sorunum yok diyelim. En azından Python ve Javascript temelinden ayrılmadığım için benim için çok farklı gelmiyor. Ki zaten Django'yu öğrenmiş ama kısmen unutmuştum. Bugün biraz bilgi tazeleme oldu benim açımdan. Şimdi sizinde unuttuklarınızı hatırlamanız ya da bilmiyorsanız belki de öğrenmeniz için oturdum adım adım yazdım.

Öncelikle bilgisayarınızda python, pip ve django kurulu olmalı. Python ve pip kurulu ise djangoyu
{% highlight bash %}sudo pip install django{% endhighlight %}
diyerek kuruyoruz. Sonrasında ise yeni projeyi bulunduracağımız dosyanın içinde aşağıdaki komutu çalıştıralım.
{% highlight bash %}django-admin startproject projeadi{% endhighlight %}
Dosyaları biraz karıştırın. Bende karıştırayım. Dikkat edilecek manage.py dosyası var. Kendisi sağolsun önemli komutlar çalıştırıyor.
Mesela;
{% highlight bash %}python manage.py runserver{% endhighlight %}
dediğimizde yerel bir web sunucusu çalıştırıyor localhostta. Varsayılan olarak 8000 numaralı portta çalışıyor.<br>
settings.py ---> ayar dosyası isminden anlaşılacağı gibi<br>
urls.py ---> routing/yönlendirme işleri için

Bir uygulamanın parçaları şu şekilde;

models.py --> veri katmanı <br>
admin.py --> admin arayüzü <br>
views.py --> kontrol katmanı <br>
tests.py --> uygulama testleri <br>
migrations/ --> veritabanı işlemleri için dosyalar <br>

İlk uygulamamızı aşağıdaki komutla oluşturalım.
{% highlight bash %}python manage.py startapp uygulamaadi{% endhighlight %}
Yeni dosyalarımız oluştu bile. Şimdi uygulamamızı settings.py dosyası içine yazalım. settings.py içinde INSTALLED_APPS kısmına 'uygulamaadi', şeklinde bir ekleme yapalım. <a href="http://www.djangoproject.com">Django Project</a> websitesinden Documentation kısmından daha detaylı bilgilere ulaşabilirsiniz. <br>
settings.py içinde önemli birkaç yer var. <br>
INSTALLED_APPS --> uygulamaları eklediğimiz yer <br>
TEMPLATES --> şablonları eklediğimiz yer <br>
STATICFILES_DIR --> css gibi statik dosyaları eklediğimiz yer <br>
DEBUG --> deploymentta false yapılması iyi bir iş olur :) <br>
DATABASES --> postgre, mysql falan kullanıldığında değiştirmeniz gereken kısım.

--MODELLER--

->Uygulamanın veri katmanı <br>
->Veritabanı yapısını tanımlar <br>
->Veritabanına sorgu yapmayı sağlar. <br>
->models.py dosyasındadır <br>

Örnek bir models.py dosyası;
{% highlight python %}
from django.db import models

class Item(models.Model):
    title= models.CharField(max_length=200)
    description = models.TextField()
    amount = models.IntegerField()
{% endhighlight %}

Çok basit bir sınıf yapısı var. Bunu ilk yazdığımızda hemen veritabanında karşılık gelen sınıf oluşturulmuyor. Bunun için migration denilen bir olay var. Modeller veritabanının yapısını belirlerken migration veritabanı yapısını değiştirmek için betikler üretir. Yeni bir model eklenince, yeni alan eklendiğinde, alan çıkarıldığında, bir alanın özelliği değiştirildiğinde migration gereklidir.

Bu kadar bahsettik. Migration nasıl yapılır. 2 komutu var manage.py sağolsun.
{% highlight bash %}
python manage.py makemigrations
{% endhighlight %}
-> sonradan kullanılmak üzere migration dosyalarını üretir.<br>
-> varolan model alanları ile varolan veritabanı tablolarını kullanır.<br>
{% highlight bash %}
python manage.py migrate
{% endhighlight %}
-> çalıştırılmamış bütün migration dosyalarını çalıştırır.<br>
-> --list ile geçmişi gösterir.<br>

Şimdi python manage.py migrate komutunu çalıştıralım. Böylece uygulanmamış tüm migration dosyaları veritabanına uygulanacak.
{% highlight bash %}
sudo apt-get install sqlitebrowser
{% endhighlight %}
komutu ile sqlite veritabanını görüntülemek için gereken programı indirelim. Programı açıp open database diyerek django projemizdeki sqlite veritabanımızı seçelim. Orada oluşturduğumuz sınıf uygulamaadi_item olarak görünecektir.
