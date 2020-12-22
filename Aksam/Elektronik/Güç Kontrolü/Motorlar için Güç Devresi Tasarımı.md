# Motorlar için Güç Devresi Tasarımı

Bu doküman termoelektrik modül üretiminde kullanılacak 3B yazıcı filamentini üretecek makinenin motor kontrolleri için gereken voltaj ve akım değerlerini sağlayabilmek adına yazılmıştır. Dokümanın en güncel hali [GitHub](https://github.com/electricalgorithm/TE-FilamentExtruder) üzerinde paylaşılmaktadır.

[TOC]



<div style="page-break-after: always;"></div>

## Model Aşaması

![model](/home/xyz49/Desktop/Projeler/Ballikaya/TE-FilamentExtruder/Aksam/Elektronik/Güç Kontrolü/model.jpeg)

Yapmam gereken bu devredeki tüm dirençleri bulmak. Bu sayede hem voltaj bölücü hem de akım bölücü özelliği kullanarak istediğim motora istediğim değerleri verebileceğim.

| Volt Değerleri  | Akım değerleri  |
| --------------- | --------------- |
| $V_{ss} = 12 V$ | $i_k = 1.667 A$ |
| $V_E = 8.6V$    | $i_E =2A$       |
| $V_S = 7.4V$    | $i_S = 0.56A$   |
| $V_Ç = 3.12V$   | $i_ç = 1.33 A$  |

Yukarıdaki tabloda verdiğim değerler, projede kullanılacak step motorlar ve doğru akım motorları tarafından *datasheetlerinde* verilen değerlerden alınmıştır.

<div style="page-break-after: always;"></div>

## Hesaplama

Hesaplama için aşağıdan yukarı gideceğim. $R_g = 0\Omega$ ve  $i_g = 0A$ kabulünü kullanarak devredeki ek bileşenleri yok etmeyi hedefliyorum.

* $R_Ç$'nin hesaplanması:
  $$
  2 i_Ç = \frac{V_Ç - 0V}{R_Ç} \rightarrow i_ç = \frac{3.12V}{2R_Ç} \rightarrow R_Ç = \frac{3.12V}{2i_Ç} = \frac{1.12}{2(1.33 A)}
  $$

  $$
  R_Ç = 1.1729\Omega
  $$

* $R_3$'ün hesaplanması:
  $$
  R_3 = \frac{V_S - V_Ç}{2i_Ç} \rightarrow R_3 = 1.6090\Omega
  $$

* $R_S$'nin hesaplanması:
  $$
  2i_S = \frac{V_s - 0V}{R_S} \rightarrow 2i_S = \frac{V_S}{R_S} \rightarrow R_s = \frac{V_S}{2i_S}
  $$

  $$
  R_S = 6.6071\Omega
  $$

* $R_2$'in hesaplanması:
  $$
  R_2 = \frac{V_E - V_S}{2i_Ç + 2i_S} \rightarrow R_2 = 0.3175\Omega
  $$

* $R_E$'nin hesaplanması:
  $$
  i_E = \frac{V_E - 0V}{R_E} \rightarrow R_E=\frac{V_E}{i_E} \rightarrow R_E = 4.3\Omega
  $$

* $R_1$'in hesaplanması:
  $$
  R_1 = \frac{V_{SS}-V_E}{i_E+2i_Ç+2i_S} \rightarrow R_1 = 0.5882\Omega
  $$

* $R_K$'nın hesaplanması:
  $$
  i_K = \frac{V_{SS}-0V}{R_K} \rightarrow R_K = \frac{V_{SS}}{i_K} \rightarrow R_K = 7.2\Omega
  $$
  

Tüm dirençleri bir tabloda toplayalım.

| Dirençler            |                      |                    |
| -------------------- | -------------------- | ------------------ |
| $R_K = 7.2\Omega$    | $R_1 = 0.5882\Omega$ | $R_E =4.3\Omega$   |
| $R_2 = 0.3175\Omega$ | $R_S=6.6071\Omega$   | $R_3=1.6090\Omega$ |
| $R_Ç=1.1729\Omega$   | ~                    | ~                  |

<div style="page-break-after: always;"></div>

## Modele Yerleştirme ve Simülasyon

![motor-guc-kontrol](/home/xyz49/Desktop/Projeler/Ballikaya/TE-FilamentExtruder/Aksam/Elektronik/Güç Kontrolü/motor-guc-kontrol.png)

Simülasyon programı olarak **Multism Live** kullanıldığı için motorun geleceği kısımlara dirençsiz, voltajı veya amperi etkilemeyecek bir şey eklenmesi gerekiyordu. Bunun için ben de yönünü doğru yerleştirdiğim diyotlar kullandım.

Simülasyonu başlattığımda değerler, istediğimden biraz daha farklı geldi.

![motor-guc-kontrol-simulasyon](/home/xyz49/Desktop/Projeler/Ballikaya/TE-FilamentExtruder/Aksam/Elektronik/Güç Kontrolü/motor-guc-kontrol-simulasyon.png)

<div style="page-break-after: always;"></div>

## Sorular

1. Simülasyondaki diyotlar devrenin o kısımlarındaki davranışları etkiler mi?
2. Simülasyonun sonucunun beklenen verileri vermemesinin sebebi nedir?
3. Hesaplarda bulunan dirençler endüstri standartlarından çok daha düşük, paralel bağlanarak o değerlere ulaşmak zor olacaktır. Başka nasıl bir çözüm olabilir?
4. Hesabın başında, tasarım aşamasında, $R_G$ ve $i_G$ sıfır kabul edilmişti. Bu devrenin davranışını değiştirir mi? Ona gerek var mıdır?

