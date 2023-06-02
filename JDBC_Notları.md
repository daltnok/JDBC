# Java Database Connectivity

### JDBC tutorial

---

- [https://riptutorial.com/jdbc](https://riptutorial.com/jdbc)
- [https://www.simplilearn.com/tutorials/java-tutorial/java-jdbc](https://www.simplilearn.com/tutorials/java-tutorial/java-jdbc)
- [https://intellipaat.com/blog/java-jdbc/?US](https://intellipaat.com/blog/java-jdbc/?US)
- Bütün DB türlerine göre JDBC driverlar’a [buradan](https://www.benchresources.net/jdbc-driver-list-and-url-for-all-databases/) erişebilirsiniz

## 1. Ders Başlıkları

---

- [ ]  JDBC nedir ?
- [ ]  JDBC katmanları /mimarisi ?
- [ ]  JDBC’de tanımlı Sınıflar  Nedir  , Ne sağlar ?
- [ ]  JDBC Kavramları Nelerdir ?
- [ ]  JDBC sprint kod yazımı ?

---

## JDBC Nedir ?

---

- API Nedir

> Bir web sitesinin ekonomi bilgilerini çektiği bir  başka web sitesi günümüzde kesinlikle vardır.
API bu noktada devreye girerrek bir backend ille frontent’in haberleşmesini otomatik olarak API’lar ile sağlanır.
>
- JDBC Nedir

> Java programlama dilinde yazılmış uygulamaların DB ile iletişime girilmesini sağlayan  uygulama programlama API’I dır. JDBC hemen hemrn tüm RDB  sistemlerine Sql sorgusu gönderebilmektedir.
>
- JDBC  Geçmişi

> Sun Microsystems firmasının ticari markasıdır. JDBC standartlarını  Sun microsystems belirler. Sun kendi standartlarının farklı firmalar tarafından kullanılıp JDBC driver geliştirmesine de izin verir.
>
- JDBC’nin Kullanım Amacı:

> Java dilinde yazılmış  programların  RDB ile iletişim kurabilmesi için kullanılan JAVA API’dır.
>

> DB uygulamalarının JAVA dilindeki  kodlar  ile gerçekleştirilmesini sağlar.
>

> JAVA kodlarının olduğu ide ile bağlanı kurulurken; JDBC Bazı Class ve INterface’lerden faydalanır.
>
- QA & SDET & Manuel Tester için JDBC’nin Sınırları ve kullanımı

> Manuel tester için database management system’inde  sql query çalıştırmak yeterlidir.
[Buradan](https://chat.openai.com/share/f834a736-fe06-4c93-8cab-8b909ea0e44b) manuel Tester’ların veritabanı yönetim araçlarından nasıl faydalandıkları Test ettikleri konusunda bilgi edinebilirsin.
>
- SDET için JDBC’nin önemine gelirsek;  
  →JDBC’nin Temelini SQL queryleri oluşturur.

> Biz Java programlama dilinde kodlama yapıyoruz.  Database’i manuel olarak gidip;  test edip
otomasyona bağlamamızın bir anlamı yok. Bir şekilde otomasyon testlerini yaparken databaase’e  bağlanabileceğimiz enviroment’i  Java Kodlarını yazdığımız IDE ile bağlamamız gerekiyor.
Bunu yaparken de JDBC’nin sağladığı Class ve Interface’lerden faydalanacağız.
Şimdilik Suit içine query atıp oradan ihtiyacımız olan data’yı çekeğimizi bilmemiz yeterlidir.
>

JDBC mimarisi  Mantığı  ve yapısı :

- JDBC mimarisinin Yapısını anlamak :

      JDBC çağrısı, veritabanı çağrısına dönüştürülür.
  • JDBC sürücüsü, veritabanı sunucusuna bağlanır ve komutu veritabanı sunucusuna      gönderir.
  • Veritabanı komutu gerçekleştirir.
  • Çıktıyı JDBC sürücüsüne geri gönderir.
  • JDBC sürücüsü, çıktıyı Java uygulamasına geri gönderir. Kısaca işlem böyle yapılır.

  ![JDBC mimarisi.png](Java%20Database%20Connectivity%206b1ec38d53204045a79bf38452c32fbb/JDBC_mimarisi.png)


2 kat

- Java ile yazılan sınıf ve arayüzler  ile database ilişkisini sağlar. dedik.  IDE ile database ile ortamın hazırlanması gerekiyor . Java kodları ile sql query’lerii kullanabilmel için enviroment hazırlanma aşamasında  kullanacağımız JDBS sınıflarını ele alalım.
- Java Application’da Java.sql  kütüphanesinden alınan  sınıflar ile JDBC Apı bu bağlantıyı taşırken;
  Driver Api’leri  nu sinif ve interface’leri
  db tool’larının ve DB’nin anlayacağı yapıya çevirip bunları artık hangi tool’u kullanıyorsak onu taşıyacak.

![Screen Shot 2023-05-31 at 20.45.36 PM.png](Java%20Database%20Connectivity%206b1ec38d53204045a79bf38452c32fbb/Screen_Shot_2023-05-31_at_20.45.36_PM.png)

Not : Database’den veriler SET olarak döner.
Set’te çalışmaktan zorlandığında Array’lere, list’lere dönüştürebilirsin. Bu senin Java bilgine bağlıdır.

Meta Data : Eğer database’den çekmek istediğin veriler belli bir kısımsa ve devassa dataları bölmwek istiyorsan Metadata sınıfını kullanarak bölmen gerekiyor.

## JDBC adımları Nelerdir ?

---

1. Hangi DBMS  türünde( Mysql,Sql Server, Maria DB, mongo DB)   çalışcaksak Onun JDBC  driver ismini web’de aratıyoruz.  [Buradan](https://www.benchresources.net/jdbc-driver-list-and-url-for-all-databases/) erişebilirsiniz
   JDBC API’sinin  drvier Api’siyle iletişim sağlaması için Class.forName metodunu Java.sql kütüphanesinden yazarak çağırıyoruz.

```java
Class.forName("com.mysql.cj.jdbc.Driver");

```

1. DB ile iletişimi başlatmak için yine JDBC API’sinin sağladığı get connection metodundan faydalanıyorruz.   Bu Metot , bir connection nesnesi döndürür

![Screen Shot 2023-05-31 at 21.13.58 PM.png](Java%20Database%20Connectivity%206b1ec38d53204045a79bf38452c32fbb/Screen_Shot_2023-05-31_at_21.13.58_PM.png)

1. SQL ifadeleri oluşturulur ( DML)

A. Bir sql query oluşturmak için. createStatement() metodu kullanılır.

bir obje oluşturmak için kullanılır.

![Screen Shot 2023-05-31 at 21.15.52 PM.png](Java%20Database%20Connectivity%206b1ec38d53204045a79bf38452c32fbb/Screen_Shot_2023-05-31_at_21.15.52_PM.png)

1. Gelen sonuçları işlemek gerekiyor.

   ![Screen Shot 2023-05-31 at 21.20.08 PM.png](Java%20Database%20Connectivity%206b1ec38d53204045a79bf38452c32fbb/Screen_Shot_2023-05-31_at_21.20.08_PM.png)


Java Collection Set konusunna bakınız

1. DB bağlantısı kapatılır.  kapatılmalıdır.  Açık DB her türlü veri sızıntısına kapalıdır.

   ![Screen Shot 2023-05-31 at 21.22.30 PM.png](Java%20Database%20Connectivity%206b1ec38d53204045a79bf38452c32fbb/Screen_Shot_2023-05-31_at_21.22.30_PM.png)

   Java’da Fıle ınput system - Selenium driver_close - Scan close  bilgi sızıntısı olmaması için bilginin olduğu her yerde close () Yapılır.

   Örnek DB database step definition:


![Screen Shot 2023-05-31 at 21.35.57 PM.png](Java%20Database%20Connectivity%206b1ec38d53204045a79bf38452c32fbb/Screen_Shot_2023-05-31_at_21.35.57_PM.png)

JDBC IDE ilk Baglantısı NASIL olur  ? Proje bağlantıları nasıl olmalıdır ?

---

- Cucumber ile çalışcağız. Ona göre bir framework yapısı oluşturmaya alışırsan daha iyi olur.

  ![Screen Shot 2023-05-31 at 21.35.50 PM.png](Java%20Database%20Connectivity%206b1ec38d53204045a79bf38452c32fbb/Screen_Shot_2023-05-31_at_21.35.50_PM.png)

  ![Screen Shot 2023-05-31 at 21.32.51 PM.png](Java%20Database%20Connectivity%206b1ec38d53204045a79bf38452c32fbb/Screen_Shot_2023-05-31_at_21.32.51_PM.png)

- dependencies bağımlı kütüphanelerinde JUnit olacak

  INTELLıJ pom xml yapısı 2 bağımlılık içeriyor.

    ```java
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        </properties>
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>3.8.1</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.32</version>
        </dependency>
    </dependencies>
    ```

- Sql ile IDE bağlantısımda JDBC kullanacağız ve bunun için dependencies olarak Mysql ise Mysql data connector  bağımlığını projenin pom dosyasına eklememiz gerekiyor.

  Not: Mvn repository’ye gitmeden intellijDe yazarak indirilmesini sağlanabilirsin

  ![Screen Shot 2023-05-31 at 21.59.59 PM.png](Java%20Database%20Connectivity%206b1ec38d53204045a79bf38452c32fbb/Screen_Shot_2023-05-31_at_21.59.59_PM.png)


DB Name :Heal Life Hospital

Database Access Informationtype: jdbc:mysqlhost/ip194.140.198.209

port:**3306**

Username: heallife_hospitaltraininguser

Password=PI2ZJx@9m^)3

database_nameheallife_hospitaltrainingusernameheallife_hospitaltraininguserpasswordPI2ZJx@9m^)3URL: "jdbc:mgit checysql://194.140.198.209/heallife_hospitaltraining";USERNAME= "heallife_hospitaltraininguser";PASSWORD="PI2ZJx@9m^)3;