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
API bu noktada devreye girerek bir backend ille frontent’in haberleşmesini otomatik olarak API’lar ile sağlanır.
>
- JDBC Nedir

> Java programlama dilinde yazılmış uygulamaların DB ile iletişime girilmesini sağlayan  uygulama programlama API’I dır. JDBC hemen hemen tüm RDB  sistemlerine Sql sorgusu gönderebilmektedir.
>
- JDBC  Geçmişi

> Sun Microsystems firmasının ticari markasıdır. JDBC standartlarını  Sun microsystems  Yani oracle belirler. Sun[oracle] kendi standartlarının farklı firmalar tarafından kullanılıp JDBC driver geliştirmesine de izin verir.
>
- JDBC’nin Kullanım Amacı:

> Java dilinde yazılmış  programların  RDB tool’ları ile ile iletişim kurabilmesi için kullanılan JAVA API’dır.
>

> DB uygulamalarının JAVA dilindeki  kodlar  ile gerçekleştirilmesini sağlar.
>

> JAVA kodlarının olduğu ide ile bağlanı kurulurken; JDBC Bazı Class ve Interface’lerden faydalanır.
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

- Java ile yazılan sınıf ve arayüzler  ile database ilişkisini sağlar. dedik.  IDE ile database ilişki ortamının hazırlanması gerekiyor . Java kodları ile sql query’lerii kullanabilmek için enviroment hazırlanma aşamasında  kullanacağımız JDBC sınıflarını  ve Interface’lerinialalım.
- Java Application’da Java.sql  kütüphanesinden alınan  sınıflar ile JDBC API bu bağlantıyı taşırken;
  Driver Api’leri  de sinif ve interface’leri  db tool’larının ve DB’nin anlayacağı yapıya çevirip bunları artık hangi tool’u kullanıyorsak onu taşıyacak.

### Kodlar ile DB’yi bağlayıp sorgularla çalışma adımları : 1

1. öncelikle ilk adım bir projede JDBC yardımıyla sorgularla çalışmak istiyorsak ilk edinmemiz gereken bilgi database için bağlantı bilgileridir.

### —>Lokalinizde bir database ile çalışmak isterseniz:

> connection URL : jdbc:mysql://myhost1:3306/db_name
user=root
>

> password=mypass
şeklinde de URL bilginiz olmalı. Bunu kullandığınız DBMS hangisiyse connection bilgilerinizden alabirisiniz.
>

Aşağıda daha detaylı açıklayacağım.

---

- Açık kaynak olan bir database’de lokalinizde çalışmak istiyorsanız paylaşıma açık örnek database örneklerinden 1 tanesine [buradan](https://resources.oreilly.com/examples/9780596007270/blob/master/LearningSQLExample.sql) ulaşabilir, import edebilirsiniz.

  ![Bank Test Database tables Info.png](Java%20Database%20Connectivity%206b1ec38d53204045a79bf38452c32fbb/Bank_Test_Database_tables_Info.png)


![Bank Test database schema.png](Java%20Database%20Connectivity%206b1ec38d53204045a79bf38452c32fbb/Bank_Test_database_schema.png)

### —>Remote bir database’ ile lokalde çalışmak isterseniz :

---

- Remote  bir database’de çalışacaksanız  aşağıda ihtiyacınız olan örnek bilgiler verilmiştir. Bu bilgilere ihtiyacınız olacak. JDBC için bu bilgileri DB admin ya da yetkiliden istenmeniz gerekiyor.

Kullanılan database yönetim tool’larından ( ( Oracle, Mysql ,Sql Server, Maria DB, mongo DB) ****************hangisinde çalışacaksak JDBC bağlantısı için  bir url string’ine ihtiyacımız var.
********[Buradan](https://www.codejava.net/java-se/jdbc/jdbc-database-connection-url-for-common-databases)**  her  veritabanı  için url String’ine ulaşabilirsiniz

Mysql için connection URL : **jdbc:mysql://[*host*][:*port*]/[*database*]**

> jdbc:mysql://[*host***]**/[database ismi]
>

🤜 Mysql kuruluysa default 3306 gelir.  [port] adımını atlayabilirsiniz.

Oracle için connection URL :

> jdbc:oracle:thin:@[//localhost:1521/mydatabase](notion://localhost/mydatabase)
>

Sql Server için connection URL:

> jdbc:sqlserver://[serverName[\instanceName][:portNumber]][;property=value[;property=value]]
>

| jdbc: protokol | : alt protokol | host : databese server adresi |
| --- | --- | --- |
| port: Mtsql kuruluysa default 3306 gelir. | /[database name] |  |

---

Java kodları ve veritabanı  bağlantızı yapıp sorgular çalıştırabilmek için;  ilk adım database bağlantınız yapıldıysa şimdi 2. adıma geçelim.

### Kodlar ile DB’yi bağlayıp sorgularla çalışma adımları  :2

Java uygulamamızdan yani kodlarımızı yazdığımız IDE’ye  bir MySQL veritabanına bağlanmak için öncelikle JDBC sürücüsü mysql-connector-java bağımlılığını pom.xml dosyamıza ekleyelim:

—> IDE ( intellij kullanıyorum) açıldığında pom.xml dosyasının içine  ki Maven yüklü olması gerekiyor. Pom xml     `<dependencies></dependencies>` tag’ları arasına  `mysql-connector-java`

bağımlılığını  yüklemeniz gerekiyor.

- Maven yüklü bir IDE’ye yeni bağımlılık eklemek
    1. yöntemle yapabilirsiniz
    - [https://mvnrepository.com/artifact/mysql/mysql-connector-java](https://mvnrepository.com/artifact/mysql/mysql-connector-java)
    - Maven yüklü ise pom.xml içinde `<dependencies></dependencies>` tag’ları arasına  `mysql-connector-java` yazmanız yeterli olacaktır. otomatik tamamlama ilr ilgili bağımlılık yüklenmiş olur.
      not: bağımlılıkları eklediktem sonra refresh etmeyi unutmayın. Aksi takdirde yüklenmez.


### Kodlar ile DB’yi bağlayıp sorgularla çalışma adımları  :3

- SQL Querylerini JDBC ile  Kullanma

  Yukarıda Belirtilen Temel hazırlık aşamasındaki aşamalar rbittiğine göre  JAVA kodları JDBC bağlantısı yapabilmemiz için 5 Adım tanımlarız.

    1. Bağlantı kurma
    2. [s](https://docs.oracle.com/javase/tutorial/jdbc/basics/processingsqlstatements.html#creating_statements)tatement objesi oluşturma
    3. Query’i çalıştırma
    4.  [`ResultSet` obje](https://docs.oracle.com/javase/tutorial/jdbc/basics/processingsqlstatements.html#processing_resultset_objects)sini oluşturma ve işleme
    5. Veritabanı (DB) bağlantısını kapatma

    ---

1. Bağlantı kurma
- JDBC API’nın sağladığı class ile  doğru sürücü eklenir.

```java
Class.forName("com.mysql.cj.jdbc.Driver");
```

💯Eğer veritabanı versiyonunuzu ve buna bağlı olarak doğru sürücüyü eklemek istiyorsnız önce Kullandığınız DB yönetim tool’unun “ about kısmından versiton kontrol edip sonra
benimki mysql  8.0.30 idi . Connector- jdbc dökümanından driver pathini buradaki döküman yardımı ile yazdım siz de kullandığınız veritabanı toolları ve buna uygun   yazabilirsiniz

[MySQL :: MySQL Connector/J 8.0 Developer Guide :: 7.1 Connecting to MySQL Using the JDBC DriverManager
Interface](https://dev.mysql.com/doc/connector-j/8.0/en/connector-j-usagenotes-connect-drivermanager.html)

1. Statement ifadesi  :
- [ ]  Java.sql statement interface’inden gelen bir objedir
- [ ]  Sql query’lerini çalıştırmak için kullanılır.
- [ ]  Eğer kodunuzda bir Connection nesnesiniz varsa bundan sadece bir JDBC statement elde edersiniz .

```java
public static void main(String[] args) {
        com.mysql.cj.jdbc.Driver
    }
```

---

1. DB ile iletişimi başlatmak için yine JDBC API’sinin sağladığı get connection metodundan faydalanıyorruz.   Bu Metot , bir connection nesnesi döndürür

2. SQL ifadeleri oluşturulur ( DML)

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


### HUB Bilgiler

---

- Not : Database’den veriler SET olarak döner.
  Set’te çalışmaktan zorlandığında Array’lere, list’lere dönüştürebilirsin. Bu senin Java bilgine bağlıdır.

  Meta Data : Eğer database’den çekmek istediğin veriler belli bir kısımsa ve devassa dataları                  bölmek istiyorsan Metadata sınıfını kullanarak bölmen gerekiyor.