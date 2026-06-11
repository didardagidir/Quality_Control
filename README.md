# İstatistiksel Kalite Kontrol — SPSS Analizi

![SPSS](https://img.shields.io/badge/IBM%20SPSS%20Statistics-Quality%20Control-1F3A5F)
![Veri Seti](https://img.shields.io/badge/Veri-AI4I%202020%20Predictive%20Maintenance-1C7293)
![Gözlem](https://img.shields.io/badge/N-10%2C000-555)
![Lisans (veri)](https://img.shields.io/badge/Veri%20Lisans%C4%B1-CC%20BY%204.0-green)

İstatistiksel Kalite Kontrol dersi projesi kapsamında, **AI4I 2020 Predictive Maintenance**
veri seti üzerinde IBM SPSS Statistics ile yapılan analizlerin çıktılarını, kullanılan adımları
ve yorumlarını içerir. Analizler; tanımlayıcı istatistikler, çapraz tablo, histogram, serpilme
diyagramı, değişken kontrol grafikleri (X̄–R, X̄–s, Bireysel–Hareketli Açıklık), nitel (p)
kontrol grafiği ve Pareto diyagramını kapsar.

---

## İçindekiler

- [Veri Seti](#veri-seti)
- [Analiz Özeti](#analiz-özeti)
- [1. Tanımlayıcı İstatistikler](#1-tanımlayıcı-i̇statistikler)
- [2. Çapraz Tablo (Type × Machine failure)](#2-çapraz-tablo-type--machine-failure)
- [3. Histogram (Torque)](#3-histogram-torque)
- [4. Serpilme Diyagramı (Torque × Rotational speed)](#4-serpilme-diyagramı-torque--rotational-speed)
- [5. X̄ – R Kontrol Grafiği (Torque)](#5-x--r-kontrol-grafiği-torque)
- [6. X̄ – s Kontrol Grafiği (Torque)](#6-x--s-kontrol-grafiği-torque)
- [7. Bireysel – Hareketli Açıklık (I–MR) Grafiği (Torque)](#7-bireysel--hareketli-açıklık-imr-grafiği-torque)
- [8. Nitel (p) Kontrol Grafiği (Machine failure)](#8-nitel-p-kontrol-grafiği-machine-failure)
- [9. Pareto Diyagramı (Hata Türü)](#9-pareto-diyagramı-hata-türü)
- [SPSS Sözdizimi](#spss-sözdizimi)
- [Ekran Görüntüleri (Dosya Eşleştirme)](#ekran-görüntüleri-dosya-eşleştirme)
- [Depo Yapısı](#depo-yapısı)
- [Kaynaklar](#kaynaklar)

---

## Veri Seti

**AI4I 2020 Predictive Maintenance Dataset** — sanayideki kestirimci bakım verisini yansıtan
sentetik bir veri setidir. 10.000 gözlem ve 14 değişken içerir.

| Değişken | Açıklama |
|---|---|
| `Type` | Ürün kalite sınıfı: L (düşük), M (orta), H (yüksek) |
| `Air temperature [K]` | Hava sıcaklığı (Kelvin) |
| `Process temperature [K]` | Süreç sıcaklığı (Kelvin) |
| `Rotational speed [rpm]` | Dönme hızı (dev/dak) |
| `Torque [Nm]` | Tork (Newton·metre) |
| `Tool wear [min]` | Takım aşınması (dakika) |
| `Machine failure` | Makine arızası (0/1) |
| `TWF, HDF, PWF, OSF, RNF` | Bağımsız arıza türleri (takım aşınması, ısı dağıtımı, güç, aşırı yüklenme, rastgele) |

> Bu projede analizler ağırlıklı olarak **Torque [Nm]** (değişken/nicel kontrol grafikleri),
> **Type** ve **Machine failure** (çapraz tablo, p grafiği) ile **arıza türleri** (Pareto)
> üzerinden yürütülmüştür.

## Analiz Özeti

| # | Analiz | SPSS Yolu | Çıktı | Temel Sonuç |
|---|---|---|---|---|
| 1 | Tanımlayıcı istatistikler | Analyze ▸ Descriptive Statistics ▸ Descriptives | `outputs/01_descriptives.png` | Torque ≈ normal; Rotational speed sağa çarpık |
| 2 | Çapraz tablo | Analyze ▸ Descriptive Statistics ▸ Crosstabs | `outputs/02_crosstab.png` | Genel arıza oranı %3,4; en yüksek L tipinde |
| 3 | Histogram | Graphs ▸ Legacy ▸ Histogram | `outputs/04_histogram_torque.png` | Torque çan biçimli, simetrik |
| 4 | Serpilme | Graphs ▸ Legacy ▸ Scatter/Dot | `outputs/05_scatter_torque_rpm.png` | Güçlü negatif (ters) ilişki |
| 5 | X̄ – R grafiği | Analyze ▸ Quality Control ▸ Control Charts | `outputs/06_xbar_chart.png`, `07_r_chart.png` | Süreç kontrol altında |
| 6 | X̄ – s grafiği | Analyze ▸ Quality Control ▸ Control Charts | `outputs/08_xbar_s_chart.png`, `09_s_chart.png` | Süreç kontrol altında |
| 7 | I – MR grafiği | Analyze ▸ Quality Control ▸ Control Charts | `outputs/10_individuals_chart.png`, `11_moving_range_chart.png` | Bireysel değerler sınırlar içinde |
| 8 | p grafiği | Analyze ▸ Quality Control ▸ Control Charts | `outputs/12_p_chart.png` | Arıza oranı kontrol altında |
| 9 | Pareto | Analyze ▸ Quality Control ▸ Pareto Charts | `outputs/13_pareto_failuretype.png` | İlk 3 tür ≈ %82,6 |

---

## 1. Tanımlayıcı İstatistikler

`outputs/01_descriptives.png`

| Değişken | N | Min | Maks | Ortalama | Std. Sapma | Çarpıklık | Basıklık |
|---|---|---|---|---|---|---|---|
| Air temperature [K] | 10000 | 295,3 | 304,5 | 300,005 | 2,0003 | 0,114 | −0,836 |
| Process temperature [K] | 10000 | 305,7 | 313,8 | 310,006 | 1,4837 | 0,015 | −0,500 |
| Rotational speed [rpm] | 10000 | 1168 | 2886 | 1538,78 | 179,284 | 1,993 | 7,393 |
| Torque [Nm] | 10000 | 3,8 | 76,6 | 39,987 | 9,9689 | −0,010 | −0,013 |

**Yorum:** Torque çarpıklık (−0,010) ve basıklık (−0,013) değerleri sıfıra çok yakın olduğundan
yaklaşık **simetrik/normal** bir dağılıma sahiptir. Rotational speed ise yüksek pozitif çarpıklık
(1,993) ve basıklık (7,393) ile **sağa çarpık** ve sivri/uzun kuyrukludur; bu değişken için
normallik varsayımı zayıftır.

## 2. Çapraz Tablo (Type × Machine failure)

`outputs/02_crosstab.png`

| Type | Toplam | Arıza (=1) | Tip içinde arıza % | Arızalar içinde pay % |
|---|---|---|---|---|
| H (yüksek) | 1003 (%10,0) | 21 | %2,1 | %6,2 |
| L (düşük) | 6000 (%60,0) | 235 | %3,9 | %69,3 |
| M (orta) | 2997 (%30,0) | 83 | %2,8 | %24,5 |
| **Toplam** | **10000** | **339** | **%3,4** | **%100** |

**Yorum:** Genel arıza oranı **%3,4**'tür. **L (düşük kalite)** ürünler hem en yüksek tip-içi
arıza oranına (%3,9) sahiptir hem de tüm arızaların **%69,3**'ünü oluşturur. İyileştirme
çalışmaları öncelikle düşük kalite sınıfına odaklanmalıdır.

## 3. Histogram (Torque)

`outputs/04_histogram_torque.png` — Ortalama = 39,987 · Std. Sapma = 9,9689 · N = 10.000

**Yorum:** Histogram, üst üste bindirilen normal eğriyle uyumlu, **çan biçimli ve yaklaşık
simetrik** bir görünüm sergiler. Bu, tanımlayıcı istatistiklerdeki düşük çarpıklık/basıklık
değerlerini destekler ve Torque için normallik varsayımının makul olduğunu gösterir.

## 4. Serpilme Diyagramı (Torque × Rotational speed)

`outputs/05_scatter_torque_rpm.png`

**Yorum:** Torque ile Rotational speed arasında **güçlü, negatif ve doğrusal olmayan (ters/hiperbolik)**
bir ilişki vardır: dönme hızı arttıkça tork azalır. Bu, fiziksel olarak güç ≈ tork × açısal hız
bağıntısıyla tutarlıdır (yaklaşık sabit güçte tork, hız ile ters orantılıdır).

## 5. X̄ – R Kontrol Grafiği (Torque)

`outputs/06_xbar_chart.png` · `outputs/07_r_chart.png` · Sigma seviyesi: 3

| Grafik | LCL | Merkez (CL) | UCL |
|---|---|---|---|
| X̄ (Ortalama) | 26,855 | 39,883 | 52,910 |
| R (Açıklık) | 0,000 | 22,585 | 47,756 |

**Yorum:** Hem alt grup ortalamaları hem de açıklıklar 3σ sınırları içinde dağılmaktadır; sınır
dışına çıkan nokta veya belirgin örüntü gözlenmediğinden süreç **istatistiksel kontrol altındadır**.

## 6. X̄ – s Kontrol Grafiği (Torque)

`outputs/08_xbar_s_chart.png` · `outputs/09_s_chart.png` · Sigma seviyesi: 3

| Grafik | LCL | Merkez (CL) | UCL |
|---|---|---|---|
| X̄ (Ortalama) | 26,846 | 39,883 | 52,919 |
| s (Std. Sapma) | 0,000 | 9,134 | 19,080 |

**Yorum:** s tabanlı sınırlar, R tabanlı sınırlarla neredeyse aynıdır (X̄ için UCL 52,919 ≈ 52,910).
Standart sapma grafiğinin tüm noktaları sınırlar içinde olduğundan süreç değişkenliği kararlıdır.

## 7. Bireysel – Hareketli Açıklık (I–MR) Grafiği (Torque)

`outputs/10_individuals_chart.png` · `outputs/11_moving_range_chart.png` · SPAN = 2 · Sigma: 3

| Grafik | LCL | Merkez (CL) | UCL |
|---|---|---|---|
| Bireysel (I) | 11,309 | 39,883 | 68,456 |
| Hareketli Açıklık (MR) | 0,000 | 10,747 | 35,106 |

**Yorum:** Tek tek gözlemler (alt grupsuz) ve ardışık farklar (MR) sınırlar içinde kalmaktadır.
I–MR grafiği, X̄ grafiklerine göre normalliğe daha duyarlıdır; Torque'un yaklaşık normal olması
bu grafiğin kullanımını destekler.

> **Not:** Kontrol grafiklerindeki genel ortalama (39,883), tüm veri ortalamasından (39,987)
> küçük bir farkla ayrılır; bu, grafiklerin Torque değişkeninin bir alt kümesi üzerinde
> (x‑ekseninde ≈100 alt grup / ≈500 gözlem) üretildiğini gösterir.

## 8. Nitel (p) Kontrol Grafiği (Machine failure)

`outputs/12_p_chart.png` · Sigma seviyesi: 3

| | Değer |
|---|---|
| Üst Kontrol Sınırı (UCL) | ≈ 0,08 |
| Merkez (p̄) | ≈ 0,03 |
| Alt Kontrol Sınırı (LCL) | 0,00 |

**Yorum:** Kusurlu (arızalı) oranı için p grafiğinde merkez çizgisi ≈ 0,03 olup, genel arıza
oranıyla (%3,4) tutarlıdır. Alt grup oranlarının tümü UCL'nin (≈0,08) altında kaldığından arıza
oranı **kontrol altındadır**; LCL negatif çıktığı için 0 alınmıştır.

## 9. Pareto Diyagramı (Hata Türü)

`outputs/13_pareto_failuretype.png` — *Cases weighted by Frekans*

| Hata Türü | Frekans | Pay % | Kümülatif % |
|---|---|---|---|
| HDF (Isı dağıtımı) | 115 | %30,8 | %30,8 |
| OSF (Aşırı yüklenme) | 98 | %26,3 | %57,1 |
| PWF (Güç) | 95 | %25,5 | %82,6 |
| TWF (Takım aşınması) | 46 | %12,3 | %94,9 |
| RNF (Rastgele) | 19 | %5,1 | %100,0 |
| **Toplam** | **373** | %100 | |

**Yorum:** İlk üç hata türü (**HDF + OSF + PWF**) toplam arızaların **%82,6**'sını oluşturur
("hayati az"). İyileştirme kaynakları öncelikle ısı dağıtımı, aşırı yüklenme ve güç arızalarına
yönlendirilmelidir.

---

## SPSS Sözdizimi

Çıktılarda görünen, kontrol grafiklerini üreten SPSS komutları:

```spss
* X-bar / s grafiği (Torque, 5'erli alt gruplar).
SPCHART
  /XS=TorqueNm BY Alt_Grup_5
  /CAPSIGMA=SBAR
  /SIGMAS=3
  /MINSAMPLE=2.

* Bireysel - Hareketli Açıklık (I-MR) grafiği (Torque).
SPCHART
  /IR=TorqueNm
  /SPAN=2
  /SIGMAS=3.
```

> X̄–R, p ve Pareto çıktılarının sözdizimini de `Paste` ile alıp bu bölüme ekleyebilirsiniz.

## Ekran Görüntüleri (Dosya Eşleştirme)

Aşağıdaki tablo, yüklediğiniz ekran görüntülerini bu README'de kullanılan önerilen adlarla
eşleştirir. Görselleri `outputs/` klasörüne bu adlarla koyabilir veya README'deki yolları
kendi dosya adlarınıza göre güncelleyebilirsiniz.

| Önerilen ad (`outputs/`) | İçerik | Orijinal dosya |
|---|---|---|
| `01_descriptives.png` | Tanımlayıcı istatistikler | `Screenshot_2026-05-29_142151.png` |
| `02_crosstab.png` | Çapraz tablo (Type × Machine failure) | `Screenshot_2026-05-29_142245.png` |
| `03_crosstab_full.png` | Çapraz tablo + Case Processing | `Screenshot_2026-05-29_142254.png` |
| `04_histogram_torque.png` | Torque histogramı | `Screenshot_2026-05-29_142414.png` |
| `05_scatter_torque_rpm.png` | Serpilme (Torque × rpm) | `Screenshot_2026-05-29_142937.png` |
| `06_xbar_chart.png` | X̄ grafiği | `Screenshot_2026-05-29_144327.png` |
| `07_r_chart.png` | R grafiği | `Screenshot_2026-05-29_144333.png` |
| `08_xbar_s_chart.png` | X̄ (s tabanlı) grafiği + sözdizimi | `Screenshot_2026-05-29_144357.png` |
| `09_s_chart.png` | s grafiği | `Screenshot_2026-05-29_144403.png` |
| `10_individuals_chart.png` | Bireysel (I) grafiği + sözdizimi | `Screenshot_2026-05-29_144503.png` |
| `11_moving_range_chart.png` | Hareketli açıklık (MR) grafiği | `Screenshot_2026-05-29_144509.png` |
| `12_p_chart.png` | p grafiği (Machine failure) | `Screenshot_2026-05-29_150056.png` |
| `13_pareto_failuretype.png` | Pareto (Hata türü) | `Screenshot_2026-05-29_162330.png` |

<!-- Görselleri README içinde göstermek için örnek (dosya adlarını güncelleyin):
![Tanımlayıcı istatistikler](outputs/01_descriptives.png)
![Torque histogramı](outputs/04_histogram_torque.png)
![X-bar grafiği](outputs/06_xbar_chart.png)
![Pareto](outputs/13_pareto_failuretype.png)
-->

## Depo Yapısı

```
.
├── README.md
├── outputs/                       # SPSS ekran görüntüleri (yukarıdaki tablo)
│   ├── 01_descriptives.png
│   ├── 02_crosstab.png
│   ├── ...
│   └── 13_pareto_failuretype.png
├── data/                          #veri dosyası
│   └── ai4i2020.csv / .sav
└── syntax/                        # SPSS sözdizimi
    └── control_charts.sps
```

## Kaynaklar

- **Veri seti:** AI4I 2020 Predictive Maintenance Dataset [Dataset]. (2020). *UCI Machine Learning Repository.* https://doi.org/10.24432/C5HS5C (CC BY 4.0).
- Matzka, S. (2020). Explainable Artificial Intelligence for Predictive Maintenance Applications. *2020 Third International Conference on Artificial Intelligence for Industries (AI4I)*, 69–74. https://doi.org/10.1109/AI4I49448.2020.00023
- Montgomery, D. C. (2019). *Introduction to Statistical Quality Control* (8th ed.). Wiley. — Böl. 6 (değişken grafikler), Böl. 7 (nitel grafikler), Böl. 5 §5.3 (Pareto).
- Şenol, Ş. (2012). *İstatistiksel Kalite Kontrol*. Nobel Yayın Dağıtım.

---

<sub>Bu README, İstatistiksel Kalite Kontrol projesinin SPSS analizi bölümü içindir. Tüm değerler,
yüklenen SPSS çıktılarından alınmıştır.</sub>
