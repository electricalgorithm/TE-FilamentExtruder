# Genel Hatları ile 3B Yazıcıları Kullanarak TE Üretimi

1. Öncelikle toz halindeki $\ce{Bi2Te3}$ (parçacık boyutu: $\lt 44\ \mu m$) ve ABS polimeri (parçacık boyutu: $\approx 400 \mu m$) bir tür mikser ile karıştıracağız. Bu mikser de bizim üretimimiz olacak. Karıştırmanın oranı ise aşağıda gösterildiği gibi olacak.
   $$
   \frac{m_{\ce{Bi2Te3}}}{m_{ABS}} = \%80
   $$

2. Bu toz karışım otomatik olarak veya el ile **tek vidalı** ekstruder makinesinin içine konulacak. Ekstruderin sıcaklığı $\approx220^{\circ}C$ ayarlı olmalı. Ekstruderin hız ve boyut ayarları konuşulmalı. Bu ektruderin vidasını döndürmek için bir tane motor bağlı olması gerekiyor. Ekstruder makinesi için detaylı bir seminer videosunu burada bulabiliriz: https://www.youtube.com/watch?v=08_f5BRYcyM

   1. Malzemenin ısıtılacağı yol boyunca sıkışıklık yaratmayı hedeflemeliyiz. Bu hedefe ya vidanın adım aralıklarının gittikçe daralması yolu ile ya da vida ile kovan arasındaki boşluğun gittikçe daralması ile ulaşabiliriz. Bu sıkışıklık bir baskı yaratacak ve malzemenin erime sürecine katkıda bulunacaktır.
   2. Malzemenin yol boyunca ısı alması ve sıcaklığının erime noktasına gelmesi için kelepçe veya spiral rezistans kullanabiliriz. Kelepçe rezistansları (İng. band resistor) seçerken içlerinde sıcaklık sensörü var mı diye kontrol etmeyi unutma, genelde oluyor. Ayrıca birkaç tane olan bu kelepçeleri sırası ile koymalı ve sıcaklığı kademe olarak arttırmalıyız.
   3. Ekstruderin kovanının paslanmaz çelikten olması öneriliyor. Unutulmamalıdır ki, paslanmaz çelik olması ısının kovan boyunca iletimini yavaşlatacaktır. Eğer bulunursa dikişsiz boru da olur, ancak üzerine düşünülmesi gerekiyor. Vida için de "ağaç delme" matkap uçları kullanılabilir.
   4. Ektruderin ucu için **kör tapa** kullanabiliriz. Aynı zamanda HepsiBurada'da pirinçten memeler de var. Bu kör tapadan önce ise yabancı siteler ve videolar genelde bir tane delikli plaka (İng. breaker plate) kullanmayı tavsiye etmiş. Bu plakanın amacı tozu tutmak, malzemeyi karıştırmak ve oluşabilecek kabarcıkları tutmakmış. Plaka için bir tür musluk ağzı kullanılabilir.
   5. Çıkan filament yaklaşık olarak $\approx 220^{\circ} C$ olacağından, ekstrudere ek olarak bir soğutma sistemine ihtiyaç var. Bunu birden fazla fan kullanarak veya su ile yapabiliriz. Su ile yapacaksak pompa almamız gerekecek, fanlar ile yaparsak ise fanları almamız gerekecek. Fanları mikrokontrol kartı ile kontrol etmemiz daha kolay olabilir, bir tahmin.

3. Ekstruderin çıkışından alınan filament uygun bir çapta olamayabileceğinden dolayı, çekici makara (İng. puller roller) sisteminden önce ve sonra olmak üzere iki tane çap ölçer makineye ihtiyacımız olacak. Bu çap ölçerler şu videodaki gibi çalışabilir: https://www.youtube.com/watch?v=tTV52DihPTc. Kodlar ve 3B model dosyaları videonun açıklamasında da verilmiş üstelik.

   1. Bu makinenin çalışma prensibinde lastik derinliği ölçer kullanılmış. Mümkün mertebe hassas olan seçilmiş. İlgili videodaki derinlik ölçer HepsiBurada'da 82₺'ye var: https://www.hepsiburada.com/oto-eko-lastik-derinlik-olcer-dis-kalinlik-derinlik-olcme-kumpasi-dijital-lcd-ekranli-p-HBV00000RQUFA. Eğer bulamazsak, yenilerinde çıkış olarak haberleşme bağlantıları olup olmadığına dikkat etmeliyiz. Adamın attığı linkten (Ebay) 4$'a Türkiye'ye ücretsiz gönderim ile sahip olabiliriz ayrıca.

4. Bir diğer önemli makine ise çekici makara sistemi. Bu makara sistemi üst üste iki tane yarı-yumuşak silindirden birinin step motor ile (ayarlanabilir olması çap ayarı için önemli - step motorun diğer motorlardan farkına bakmalıyız) döndürülmesi prensibine dayanıyor. Bu sistem için Making Stuff kanalının [#5](https://www.youtube.com/watch?v=UkPja5LeuoE) ve [#6](https://www.youtube.com/watch?v=gyy7zwMgzdw)'ıncı videoları çok işe yarar.

5. Son olarak ise makaraya toplayıcı sistem gerekiyor. Bu sistemde de bir tane motor kullanılacak. Sistemin tek amacı makaranın etrafına oluşturulan filamenti toplamak olacak. Bunun için sıra ile ve düzgün toplanması için ihtiyaca göre makaranın kendisine ileri geri hareketi yapması için bir sistem de tasarlanabilir.

```mermaid
graph LR
A("Malzeme Karıştırıcısı") --> B("Extruder Makinesi")
B --> C["Çap Ölçümü 1"]

G[Çap Ölçümü 1] --> D("Çekici Makara Sistemi")
D --> E["Çap Ölçümü 2"]
E --> F("Makaraya Toplama")
```

Eğer ki makinenin amacı yalnızca filament üretmek değil, 3B yazıcı ile bu filamenti kullandırtmak ise, o zaman 3B yazıcı ile TE'li polimer ile bir ürün ortaya çıkardıktan sonra sinterleme işlemini de göz önüne almalıyız. Sinterleme için en verimli sıcaklık $500^{\circ} C$ olarak hocanın makalesinde görülmektedir. Sinterleme işleminin ardından ürün oksitlenmeye kolay  maruz kalabildiği için sinterleme işlemi yüksek saflıktaki argon gazı ile yapılmalı ve daha sonra kurşun kaplar içinde saklanmalıdır.

## Sorular

* Mikserdeki karıştırma oranı doğru şekilde mi anlaşılmıştır?
* Mikserden aldığımız karışımı direk olarak ektruderin ağzına göndermeli miyiz? Yani tam otomasyon sağlanmalı mı?
* Ekstruderin hız ve boyut ayarlarını yüksek ihtimalle bulduğumuz kovana göre veya ağaç delme matkabına göre karar vereceğiz. Bu detayları proje dokümanında vermemiz gerekir mi, gerekirse nasıl verelim? "Ekstruderin hızı, çap ölçüm sistemlerinden aldığımız veriye bağlı olan bir fonksiyon aracılığı ile değişecektir." yazmak yeterli olur mu?
* Kovanın içindeki o vidanın herkes sıkışıklık yaratmasını önermiş. Bazıları gittikçe adım genişliğini daraltmış bazıları ise adımın derinliğini azaltmış. Biz bunu nasıl yapabiliriz? Ağaç delme uçları tekdüze şekildeler. Veya bunu sağlamayı önemsemeli miyiz?
* Kovanın paslanmaz çelikten olduğu durumun avantajları var, ama dezavantajları da var. Paslanmaz çelik boruların ısıl iletkenliği $\approx 15\ W m^{-1} K^{-1}$  iken çelik boruların ısıl iletkenliği $\approx 52\ Wm^{-1}K^{-1}$ imiş. Dikişsiz boru seçmeyi  planlıyor muyuz? Okuduğum kadarı ile dikişsiz boruların basınca karşı dayanıklılığı yüksek olduğu için ağır sanayide o tercih ediliyormuş.
* Soğutma sistemi için fan mı su mu kullanılacak yoksa ikisi birden mi?
* Kalın bir filamenti (ben hayal edemedim de) çekici makara sistemine soktuğumuzda ve makaraların hızını artırdığımızda çıkışta daha mı ince olacak yoksa daha mı kalın olacaktır bu filament?
* Toplayıcı makaranın nizami bir şekilde toplamasını istiyor muyuz yoksa fazladan uğraş yaratacağı için sistemin çalışması bizim için yeterli mi?
* Filamentin kullanım ve sinterleme aşaması bizim proje konumuza dahil midir?