---
layout: post
title:  "Salesforce Unit Test Yazımı - Salesforce (1)"
date:   2015-10-22 00:01:00
categories: salesforce apex unittests test
---
Yaklaşık 1,5 yıldır Force.com Developer olarak çalışıyorum. Salesforce nedir ne değildir başka bir yazımda anlatacağım. Salesforce konusunda pek Türkçe kaynak bulunmadığı için bir yerlerden ben başlayayım diye düşündüm. Peki neden testlerden başlıyorum. Bu çok iyi bir soru. -Tebrik ediyorum sizi böyle güzel bir soru için.- Hemen yanıt vereyim. Salesforce production ortamına kodları aktarmak için en az %75 code coverage dediğimiz kodların üzerinden geçilmesi olayını zorunlu tutmuş. Bugüne kadar çoğu zaman aman şu code coverage tutsun da başka şey istemem diye aslında test sayılmayan çok fazla test yazmışlığım var. Çünkü Salesforce hızlı geliştirme yapılabilmesi ile önemli ve test yazmayı zaman kaybı olarak görüyordum. -Tamam vurmayın.-

Hataları yakalamak için testleri hep arayüzden yapıyordum. Bu çalışıyor mu çalışıyorsa istenen şeyi yapıyor mu şöyle bir değer versem nasıl çalışır testleri bahsettiğim. Code coverage yakalamak içinse basit basit şeyler yazıyordum. Aslında unit testler ile test senaryolarını uygulayabileceğimi ve bunun en mantıklı ve hızlı ve sonradan kullanılabilir yöntem olduğunu öğrenmem biraz zaman aldı. Benim hatam ama sonuçta insan hatalarından geçte olsa bir şeyler öğreniyorsa bence sorun yok demektir. -Sizce sorun olabilir, haklısınız.-

Salesforce'ta unit test yazmak aslında çok basit. Test verisini üret. İstediğin fonksiyonları çağır. Ta-da. Oldu bile. Bu kadar makara yeter. Şimdi nasıl yazacağımıza geçelim. Öncelikle istediğiniz geliştirme ortamından (istediğiniz derken benim bildiğim 4 farklı yer var; Salesforce'un arayüzü, Salesforce'un developer konsolu, Eclipse'deki Force.com IDE ve Sublime Text'deki plugin) Ben genelde Salesforce'un developer konsolunu tercih ediyorum. Diğer yöntemlere göre daha hızlı bana göre. Bir de bunu kullanarak alıştığım için diğerlerini kullanmak zor geliyor. Eclipse'de Force.com IDE'yi büyük projelerde gereken yerleri araştırmak için kullanıyorum. -Tüm projeyi arama özelliği tanrı vergisi resmen- Örnek bir Apex sınıfı için bir unit test yazalım şimdi. Sınıfımız basit bir işlem yapsın.

public class CevreHesaplama {
    public static Integer kareninCevresi(Integer a) {
      Integer cevre = 4*a;
      return cevre;
    }
}

Bu sınıfı test edelim şimdi.

@isTest
public class CevreHesaplamaTest{
  @isTest static void kareninCevresiTest(){
    Integer cevre = CevreHesaplama.kareninCevresi(4);
    system.assertEquals(cevre, 16);
  }
}

Test etmek için developer konsolda Test -> New Run -> CevreHesaplamaTest -> Run şeklinde testimizi çalıştırabiliriz. Çalıştırınca testimizin geçtiğini ve code coverage denen arkadaşın CevreHesaplama sınıfı için %100 olduğunu göreceğiz. Şimdi bu test yeterli mi sizce sayın okur? Şöyle düşünelim. Son kullanıcı dediğimiz arkadaşlar her zaman bu kadar düz mantıkla hareket etmiyorlar. Yani çevre hesaplanırken oraya yazı giren olur (örneğin; dört), negatif sayı girmek isteyen olur, ondalıklı sayı girer. Olur bunların hepsi. Bizim bunları önceden test etmemiz ve buna göre önlemimizi almamız gerekir.

Salesforce'da test sınıfları veritabanındaki kayıtlara erişemez. O sebeple test verilerini kod içinde üretiriz. Sadece Kullanıcı ve Profil sınıflarının verileri test sınıflarından erişilebilirdir. Hiç tavsiye edilmeyen bir yöntem olarak  @isTest(SeeAllData=true) şeklinde veritabanı verilerine test sınıfından erişebilirsiniz. Ama yanlış bir şey yaparsanız sonra üzülmeyin derim ben. Bunun varlığını unutun. Ben şu ana kadar hiç kullanmadım desem yeridir.

Bunlar dışında test sınıfları ile ilgili birkaç ufak bilgi vereyim.<br>
->Test sınıfları mail göndermezler.<br>
->Test sınıfları üçüncü parti web servislerine çağrı yapmazlar. Bunun için WebServiceMock sınıfını kullanmak gerekir.

Şimdilik testlerle ilgili bahsedeceklerim bu kadar. İlerleyen günlerde testlerde dahil olmak üzere daha ayrıntılı yazılara devam edeceğim.
