# GlobalAI_Mart_2025
# Sürücüsüz Metro Simülasyonu (Rota Optimizasyonu)

## Proje Hakkında
Bu proje, bir metro ağında iki istasyon arasındaki **en az aktarmalı rotayı (BFS)** ve **en hızlı rotayı (A*)** bulmayı amaçlamaktadır. Proje dosyaları incelendiğinde, bazı sınıfların (`Istasyon`, `MetroAgi`) ve yapıların (`komsular`, `istasyonlar`, `hatlar`) önceden tanımlandığı görülmüştür.

Projede, geliştiriciden **BFS algoritmasını (en az aktarmalı rota bulma)** ve **A* algoritmasını (en hızlı rota bulma)** kendi metotları olarak tamamlaması istenmiştir.

## Kullanılan Teknolojiler ve Kütüphaneler
- **Python 3** - Projenin ana dili
- **collections.deque:** BFS algoritmasında kuyruk yapısı oluşturmak için kullanıldı.
- **heapq:** A* algoritmasında öncelik kuyruğu oluşturmak için kullanıldı.
- **typing:** Tür belirlemeleri için (`Optional`, `List`, `Tuple`)

## Algoritmaların Çalışma Mantığı

### 1. En Az Aktarmalı Rota Bulma (`en_az_aktarma_bul` - BFS)
**BFS algoritması**, her adımda istasyonları genişleterek tüm olasılıkları keşfeder. İstasyonlar, bir **FIFO Kuyruğu (`deque`)** yardımıyla sırayla ziyaret edilir.
- **Başlangıç İstasyonu** doğrudan `ziyaret_edildi` listesine eklenir.
- Her adımdaki komşular, daha önce ziyaret edilmediyse kuyruğa eklenir.
- Hedefe ulaşıldığında, rota döndürülür.

Bu algoritma, en kısa (en az aktarmalı) rotayı bulmada garantilidir.

### 2. En Hızlı Rota Bulma (`en_hizli_rota_bul` - A*)
**A* algoritması**, her adımda maliyeti en düşük olan istasyonu seçerek ilerler. 
- Kullanılan yapı: **Öncelik Kuyruğu (`heapq`)**.
- Her adımdaki toplam süre hesaplanır ve bu süreye göre istasyonlar sıraya yerleştirilir.
- `ziyaret_edildi` listesi kullanılarak, aynı istasyonun birden fazla ziyaret edilmesi önlenir.
- Hedefe ulaşıldığında, rota ve toplam süre döndürülür.

Bu algoritma, zaman bazlı en hızlı rotayı bulmayı sağlar.

## Neden Bu Algoritmalar Kullanıldı?
- **BFS (Breadth-First Search):** Düz bir arama algoritması olup, en kısa yolu (aktarma sayısını) bulmak için garantili bir çözümdür.
- **A* (A-Star):** Önceliklendirilmiş arama algoritması olup, süre bazlı en iyi rotayı bulmak için daha verimlidir.

## 📌 Örnek Kullanım ve Test Sonuçları
```python
    # AŞTİ'den OSB'ye En Az Aktarmalı Rota
    rota = metro.en_az_aktarma_bul("M1", "K4")
    if rota:
        print("En az aktarmalı rota:", " -> ".join([istasyon.ad for istasyon in rota]))

    # AŞTİ'den OSB'ye En Hızlı Rota
    sonuc = metro.en_hizli_rota_bul("M1", "K4")
    if sonuc:
        rota, sure = sonuc
        print(f"En hızlı rota ({sure} dakika):", " -> ".join([istasyon.ad for istasyon in rota]))
```

## Ek Test Senaryoları
Aşağıdaki ek senaryolar, algoritmaların farklı durumlarda nasıl çalıştığını test etmek için kullanılmıştır:

- **OSB'den Batıkent'e:** En hızlı rota: 18 dakika
- **Gar'dan Kızılay'a:** En hızlı rota: 9 dakika
- **Demetevler'den AŞTİ'ye:** En hızlı rota: 17 dakika

Bu testler, algoritmaların doğru çalıştığını ve beklenen sonuçları verdiğini göstermektedir. Daha fazla test eklenerek algoritmaların güvenilirliği artırılabilir.

## Projeyi Geliştirme Fikirleri
- **A* Algoritmasına Heuristik Ekleme:** Şu anda A* algoritması sadece toplam süreyi değerlendiriyor. Eğer bir `heuristic` fonksiyonu eklenirse, algoritma daha verimli çalışabilir.
- **Rotaların Görselleştirilmesi:** Bulunan rotaların grafiksel olarak çizilmesi daha anlaşılır bir çıktı sağlayabilir.
- **Test Kapsamını Artırma:** Daha fazla test senaryosu eklenerek algoritmaların doğruluğu ve verimliliği ölçülebilir.

- **İletişim için:** cagrialtinuzengi@gmail.com