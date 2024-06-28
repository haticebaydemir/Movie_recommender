## Projenin kodlarına [buraya tıklayarak](https://colab.research.google.com/drive/1Dw_2zYm9PRjWuTP9pDepeAfin9oXweWg) ulaşabilirsiniz.
# movie_recommender
İçerik Tabanlı Filtreleme (Content-Based Filtering)

```from google.colab import drive
drive.mount('/content/drive')
import pandas as pd
movies = pd.read_csv('/content/drive/MyDrive/movie/dataset.csv')
movies.head(10)
movies.describe()
movies.info()
movies.isnull().sum()
movies.columns
movies=movies[['id', 'title', 'overview', 'genre']]
#veri setini küçültmek ve işlemlere uygun hale getirmek için özellikleri(features) sınırlandırıyoruz.
movies
movies['tags'] = movies['overview']+movies['genre']
#Verilerin daha derin analizlenebilmesi için overview ve genre özelliklerini birleştirip 'tags' olarak yeni bir özellik oluşturuyoruz.
movies
new_data  = movies.drop(columns=['overview', 'genre'])
#Veri setimizden overview ve genre özelliklerini çıkarıyoruz.
new_data
from sklearn.feature_extraction.text import CountVectorizer
#Metin verilerini sayısal vektöre çevirmek için bu kütüphaneyi kullanıyoruz.
cv=CountVectorizer(max_features=10000, stop_words='english')
#Gereksiz verilerle uğraşmamak için maximum 10,000 özellik ile sınırlandırıyoruz ve en fazla kullanılan kelimeler ('english' gibi) hesaba katılmaması için stop words olarak belirtiyoruz.
cv
vector=cv.fit_transform(new_data['tags'].values.astype('U')).toarray()
#Metin verilerimizi sayısal vektöre dönüştürdük.
vector.shape
from sklearn.metrics.pairwise import cosine_similarity
#Yakınlığı ölçmek için bu kütüphaneyi kullanacağız.
similarity=cosine_similarity(vector)
#Yakınlığı(benzerliği) ölçmek için kosinüs yakınlığını kullanıyoruz.
#Vektörlerin aynı yöne ne kadar baktığını ve aralarındaki açıya bakarak benzerliklerini ölçer.
similarity
new_data[new_data['title']=="The Godfather"].index[0]
distance = sorted(list(enumerate(similarity[2])), reverse=True, key=lambda vector:vector[1])
for i in distance[0:10]:
    print(new_data.iloc[i[0]].title)
#Bu verileri benzerlik oranı azalan sırayla list haline getirip sonra yazdırıyoruz.
def recommand(movies):
    index=new_data[new_data['title']==movies].index[0]
    distance = sorted(list(enumerate(similarity[index])), reverse=True, key=lambda vector:vector[1])
    for i in distance[0:10]:
        print(new_data.iloc[i[0]].title)
         #Print ile önermeyecek, ürettiklerini 1 dizide birleştirip return edecek. Biz de bu return edilen diziyi aşağıda kullanacağız.
         #Öneri sistemimizin çalışması için recommand fonksiyonunu oluşturduk.
recommand("Iron Man")
import pickle
pickle.dump(new_data, open('movies_list.pkl', 'wb'))
#nesneyi movies_list.pkl adlı dosyaya kaydeder
pickle.dump(similarity, open('similarity.pkl', 'wb'))
#benzerlik matrisi similarity.pkl adlı dosyaya kaydedilir.
pickle.load(open('movies_list.pkl', 'rb'))
#kaydedilen nesneyi tekrar okumak için kullanıyoruz.
recommand("Star Wars")
recommand("The Godfather")
```

Filmlerin afişini görüntülemek için API'den yardım alarak ekstra bir şeyler yapabiliriz.

```
import http.client
conn = http.client.HTTPSConnection("api.collectapi.com")
import json

def bringPoster(filmName):
  headers = {
      'content-type': "application/json",
      'authorization': "apikey 02pZAmvOqYcTp9FgVhALMm:6yMhJCAMU2NwWU23rEtpJL"
      }
  conn.request("GET", "/imdb/imdbSearchByName?query="+filmName, headers=headers)
  res = conn.getresponse()
  data = res.read()
  jsonData = json.loads(data)
  poster = jsonData['result'][0]['Poster']
  return poster
recommendedArray = ["Titanic","Narcos","Shrek"] #Bu bizim uydurduğumuz sonuç dizisi
for film in recommendedArray:
  print(bringPoster(film)) #Bu kısımda da yeni bir diziye aşağıda ki çıktı olan poster linklerini eklersen sonrasında poster linklerine ulaşabileceksin.```
