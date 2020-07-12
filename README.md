# Git Versiyon Kontrol Sistemi Rehberi
Git, küçük ya da çok büyük ölçekli projelerde her şeyi hızlı ve verimli bir şekilde idare edebilmek için tasarlanmış ücretsiz ve açık kaynaklı dağıtık bir sürüm kontrol sistemidir.

![GIT](https://git-scm.com/images/logo@2x.png)

## 1. Başlangıç
Bir proje geliştirirken yazdığınız kod üzerinde yeni düzenlemeler yaparken mutlaka yanlışlıklar yaptığınız olmuştur. Bu yanlışlıklar eğer çalışmanızın yedeği yoksa sizi bunu düzeltmekle uğraştıracaktır ya da birden çok kişinin çalıştığı bir projede aynı kod üzerinde çalışırken eklenenleri elle düzeltmek oldukça zaman alacaktır. Bu gibi şeyleri daha kolay ve doğru yapmak için Git kullanabilirsiniz. Bu bölümde Git neden kullanıldığını, çalışma mantığını ve bilgisayarımıza nasıl kuracağımızı göreceğiz. 
### 1.1 Versiyon Kontrol Sistemi Nedir?
Versiyon kontrol sistemi daha sonra geri dönebilmek üzere üzerinde çalışılan dosyalarda yapılan değişiklikleri kaydeden sistemdir. Versiyon kontrolü sayesinde üzerinde çalıştığınız projede yaptığınız yanlış bir ekleme sonucunda projenizi çok hızlı bir şekilde eski haline getirebilir, yeni özellikler eklerken yedek dosyaların oluşturduğu karmaşıklığı önleyebilirsiniz. 

### 1.2 Git Nedir?
Git, 2005 yılında Linux Geliştirme Topluluğu (Linux development community özellikle Linus Torvalds) tarafından geliştirilmiş dağıtık çalışan bir versiyon kontrol sistemidir. Git geliştirilirken hızlı olması, basit bir tasarıma sahip olması, doğrusal olmayan geliştirmeye uygun olması (non-linear devolopment), tamamen dağıtık çalışması, Linux çekirdeği gibi büyük projelerde de kullanılabilir olması hedeflenmiştir. Eclipse kullanıcı topluluğu anketi verilerine göre 2013 yılı itibarıyla %30 pazar payına ulaşmıştır. 
Çoğu versiyon kontrol sistemi çalışma dizinindeki dosyalardaki değişiklikleri kaydetme yöntemini izler bunların aksine Git, çalışma dizininde değişiklik olduğunda basitçe anlatmak gerekirse dizindeki dosyaların fotoğrafını (snapshot) çeker. Aynı zamanda değiştirilmemiş dosyaları tekrar depolamaz bu sayede verimliliği artar.
### 1.3 Neden Git?
Git, dağıtık yapısı sayesinde neredeyse tüm işlemleri için çevrimdışı olarak çalışır. Sadece üzerinde çalışacağı dosyaya erişmesi yeterlidir, Üzerinde çalıştığınız bir projede eskiye dönmek için sadece yerelinizdeki dosyalara ihtiyaç duyar. Bu da Git'in çok hızlı çalışmasını sağlar.
Çalıştığı klasörde Git'in haberi olmadan değişiklik yapılmasını önlemek amacıyla (checksummed) kullandığı mekanizma SHA-1 hash olarak adlandırılır. Bu yapı onaltılık sayı tabanında 40 karakterlik ve Git'teki bir dosya veya dizin yapısının içeriğine göre hesaplanan bir karakter dizisinden oluşur 
### 1.4 Git Kurulumu
Bu bölümde farklı işletim sistemleri için Git kurulumundan bahsedilecektir.
###### 1.4.1 Linux Git Kurulumu
Paket yükleyicisi aracılığıyla Ubuntu gibi Debian tabanlı linux dağıtımlarına git yüklemek için ```apt``` kullanabilirsiniz.
```
$ sudo apt install git-all
```

Fedora (ya da RHEL, CentOS gibi yakından ilişkili RPM tabanlı linux dağıtımı) kullanıyorsanız ```dnf``` kullanabilirsiniz.
```
$ sudo dnf install git-all
```
daha çok seçenek için Git'in resmi internet sitesini ziyaret edebilirsiniz.

###### 1.4.2 Windows Git Kurulumu
Windows'a yüklemek için https://git-scm.com/download/win bu bağlantıya tıkladığımızda kurulum dosyası otomatik olarak indirilmeye başlayacaktır. İndirilen exe dosyasını çalıştırdığınızda kurulum başlayacaktır. Ayrıca Git yüklemenin bir diğer yolu da Github Desktop kurmaktır. Github Desktop kurulduğunda Git de kurulmuş olur. [Bu bağlantıdan](https://desktop.github.com/) Github Desktop uygulamasının sitesine ulaşabilirsiniz.  
###### 1.4.3 macOS Git Kurulumu 
Git yüklemenin birçok yolu vardır. Bu yollardan biri komut satırına ```$ git --version``` yazdığımızda eğer kurulu değil ise gelen adımları takip ettiğimizde kurulmuş olacaktır. Bir diğer yöntem https://git-scm.com/download/mac adresinden en güncel Git sürümünü indirerek adımları takip etmektir ya da Github Desktop kurarak Git'i kurabilirsiniz. [Bu bağlantıdan](https://desktop.github.com/) Github Desktop uygulamasının sitesine ulaşabilirsiniz.  
### 1.5 Git Ayarlarının Yapılması
Git kurduktan sonra bazı özelleştirmeler yapmak için ve uzak kod depolarına (repository) çalışabilmek için bazı ayarlar yapmak gerekir. Bu yüzden Git, tüm ayarları yapmamızı sağlayan ve yapılandırma değişkenlerinin bulunduğu bir dosya oluşturan ```git config``` aracıyla birlikte gelir. ```git config``` aracı ile oluşturulan dosya sisteminize kaydedilerek ayarlarınız kalıcı hale gelir. 
Öncelikle ayarların kaydedildiği dosya yani gitconfig, kaydedildiği yere göre etki alanı değişebilir:
1- Bir bilgisayardaki tüm kullanıcılar tarafından kullanılması için /etc/gitconfig konumunda tutulur. ```git config --system``` kullanılarak ayarlamalar yapılır. 
2- Bilgisayardaki tüm repository'leri etkilemesi için ~/.gitconfig konumunda tutulur. ```git config --global``` kullanılarak ayarlamalar yapılır. 
3- Sadece bir repository'yi etkilemesi için .git/config ...
şeklinde depolanır. 
## 2. Git Temelleri
### 2.1 Git Repository'si oluşturmak
### 2.2 İlk Commit
### 2.3 Yapılan Değişikliği Geri Almak

## Kaynakça
1- https://git-scm.com/book/en/v2

2- https://tr.wikipedia.org/wiki/Git_(yaz%C4%B1l%C4%B1m)#cite_note-1
