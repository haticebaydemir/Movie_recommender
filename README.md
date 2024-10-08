## Projenin kodlarına [buraya tıklayarak](https://colab.research.google.com/drive/1Dw_2zYm9PRjWuTP9pDepeAfin9oXweWg) ulaşabilirsiniz.
İçerik Tabanlı Filtreleme (Content-Based Filtering)

# Movie Recommendation System
İçerik Tabanlı Filtreleme (Content-Based Filtering)
## Proje Açıklaması
Bu proje, kullanıcıların film tercihlerine dayalı olarak benzer film önerileri sunan bir öneri sistemi geliştirmeyi amaçlamaktadır. Öneri sistemi, kullanıcıların film keşif süreçlerini kolaylaştırmak için veri analizi ve makine öğrenimi tekniklerini kullanmaktadır. Proje, IMDb verilerini kullanarak film posteri ve benzerlik analizleri gerçekleştirmektedir.

## İçindekiler
- Gereksinimler
- Veri Seti
- Kurulum
- Kullanım
- Fonksiyonlar
- Sonuçlar
- İletişim
## Gereksinimler
- Python 3.x
- Pandas
- scikit-learn
- HTTP.client
- JSON
- Pickle

## Veri Seti
Proje, film verilerini içeren bir CSV dosyasından (dataset.csv) faydalanmaktadır. Veri seti aşağıdaki özellikleri içermektedir:

- **id**: Film kimliği
- **title**: Film başlığı
- **overview**: Film özeti
- **genre**: Film türü

## Kurulum
1. Google Drive'ı Bağlayın:
```bash
from google.colab import drive
drive.mount('/content/drive')
```
2. Gerekli Kütüphaneleri Yükleyin:
```bash
pip install pandas scikit-learn
```

## Kullanım
1. Film Verilerini Yükleyin ve İnceleyin:
```bash
import pandas as pd
movies = pd.read_csv('/content/drive/MyDrive/movie/dataset.csv')
print(movies.head(10))
```
2. Film Posterini Almak için *bringPoster* Fonksiyonunu Kullanın:
```bash
def bringPoster(filmName):
    # IMDb'den film posteri almak için API çağrısı
    ...
```
3. Benzer Filmleri Öneren recommand Fonksiyonunu Kullanın:
```bash
recommand("Iron Man")
```
## Fonksiyonlar 
- **bringPoster(filmName)**: Verilen film adı için IMDb'den film posteri alır.
- **recommand(movies)**: Belirtilen film adına benzer filmleri önerir ve sonuçları döndürür.

## Sonuçlar
Proje, kullanıcıların ilgi alanlarına göre benzer filmleri önererek film keşif deneyimlerini geliştirmeyi hedeflemektedir. Kullanıcılar, önerilen filmlerin posterlerine ve bilgilerine erişebilir.


# İletişim
Sorularınız veya önerileriniz için aşağıdaki iletişim bilgilerini kullanabilirsiniz:

E-posta: baydemirhatice@hotmail.com

Linkedln: https://www.linkedin.com/in/haticebaydemir/
