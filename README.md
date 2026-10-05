# Veri Analitiği & Yapay Zekâ Vaka Çalışması

Rapor: `RAPOR.md`

## Klasör yapısı

```
teslim/
├── RAPOR.md
├── README.md
├── kod/
│   ├── 0-0Analiz.ipynb
│   └── requirements.txt
└── ciktilar/
    ├── altin_set.csv          (elle etiketlenen 40 kayıt)
    ├── llm_etiketleri.csv     (200 kaydın LLM etiketleri)
```

Vaka veri dosyaları (`musteriler.csv`, `araclar.csv`, `servis_kayitlari.csv`, `geri_bildirimler.csv`) teslime dahil değildir, çalıştırmak için `veri/` klasörüne konmalıdır.

> **Not:** Notebook içerisindeki analiz sonuçları ve ilgili çıktılar kayıtlıdır; bu nedenle sonuçları görmek için notebook'u çalıştırmanız gerekmez. İsterseniz kodları çalıştırarak analiz adımlarını ve sonuçların nasıl üretildiğini de inceleyebilirsiniz. Bölüm 3'teki LLM etiketleme adımı ise Gemini sohbet arayüzü üzerinden manuel olarak gerçekleştirildiği için yeniden çalıştırılamaz.


## Ortam

Python 3.11.5. Kurulum:

```
pip install -r kod/requirements.txt
```

## Çalıştırma

1. Vaka veri dosyalarını `veri/` klasörüne koyun.
2. `kod/0-0Analiz.ipynb` dosyasını Jupyter Notebook ile açın. Dosya yolları notebook'un bulunduğu klasöre göre ayarlanmıştır.
3. Bölüm 1 ve 2 hücrelerini sırayla çalıştırın. Bölüm 3.3, Bölüm 2'de eğitilen modele (`best_log_model`), `df_analiz` tablosuna ve `ciktilar/llm_etiketleri.csv` dosyasına bağlıdır.
4. Bölüm 3.1-3.2'de dosya üreten ve ham Gemini çıktılarını okuyan hücreler teslimdeki dosyalar olmadan çalışmaz (aşağıya bakın). Sonuçlar için `llm_etiketleri.csv` ve `altin_set.csv` yeterlidir.

## Dikkat edilecekler

- **Altın set korunmalı.** 3.1'deki hücreler `altin_set.csv` dosyasını boş etiketlerle yeniden yazar. Elle etiketlenmiş dosyanın üzerine yazmamak için bu hücreleri yeniden çalıştırmayın. 3.2'deki karşılaştırma doğrudan teslim edilen `altin_set.csv` dosyasını okur.
- **LLM adımı elle yapıldı.** Etiketleme API kullanılmadan, Gemini sohbet arayüzünden 25'erli 8 grup halinde yapıldı. Bu adım notebook'ta yeniden çalıştırılamaz.
- **Örneklem.** 200 kayıt `random_state=42` ile seçildi. Aynı 200 kayıt `llm_etiketleri.csv` içindedir.
- **Teslimde bulunmayan ara dosyalar.** `orneklem_200_ham.csv`, `gruplar/` ve `llm_ham/` teslime konmadı. Gemini çıktıları `llm_etiketleri.csv` içindeki `llm_` sütunlarındadır.
- **İstemler.** Kullanılan istemlerin tam metni `RAPOR.md` Bölüm 5.2'dedir.