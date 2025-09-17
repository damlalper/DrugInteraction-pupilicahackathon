# 💊 AI-Powered Drug Interaction Checker

## 📌 Proje Amacı
Bu proje, kullanıcıların ilaç-ilaç etkileşimlerini kolayca kontrol edebileceği **AI tabanlı bir web uygulaması**dır.  
Kullanıcı, "Parol ve Nurofen aynı anda kullanabilir miyim?" gibi sorular sorduğunda:  

- NLP ile ilaç isimleri otomatik tespit edilir  
- Veri tabanındaki etkileşim bilgileri RAG yöntemiyle bulunur  
- LLM (Mistral) Türkçe, anlaşılır cevap üretir  
- İsteğe bağlı olarak **eczacıya danışma** opsiyonu sunulur  

Projenin amacı, **eczacının iş yükünü hafifletmek** ve kullanıcı dostu bir ilaç etkileşim kontrol sistemi geliştirmektir.  

---

## 🏗️ Mimari Yapı

[Frontend - React]
         |
         v
[Backend - FastAPI]
         |
         |-- [Drug DB + Vector DB] (İlaç verileri + embedding)
         |
         |-- [AI Layer]
         | |-- NLP (ilaç tanıma)
         | |-- RAG (benzer kayıt getir)
         | |-- LLM (Türkçe cevap üret)
         |
         v
    [Kullanıcıya Yanıt]



---

## 🔹 Katmanlar ve Görevler

### 1. Veri Katmanı
- CSV dosyasından (`drug1, drug2, interaction`) ilaç verileri alınır  
- **Temizleme & Normalize:**  
  - Küçük harfe çevirme  
  - Varyasyonları tekilleştirme  
- **Veri Tabanı Yapısı:**  
  - JSON / SQL / SQLite  
- **Embedding:**  
  - `drug1 + drug2 + interaction açıklaması` → vektör haline getirilir  
  - Vector DB’ye (Milvus, Weaviate, FAISS) kaydedilir  

---

### 2. Backend (FastAPI)
- **API Endpoint’leri:**  
  - `/check_interaction` → İlaçları input al, DB’den sonuç döndür  
  - `/ask_chatbot` → NLP + RAG + LLM üzerinden yanıt üret  
  - `/get_drugs` → Autocomplete için ilaç listesi döndür  

- **İşlev:**  
  - Kullanıcıdan gelen istekleri işler  
  - AI katmanıyla etkileşir  
  - Frontend’e JSON yanıt döndürür  

---

### 3. AI Katmanı
- **NLP (İlaç Tanıma):**  
  - Kullanıcı cümlesindeki ilaç isimlerini ayıklar  
- **RAG:**  
  - Vector DB’den benzer kayıtları getirir  
- **LLM (Mistral):**  
  - Context + kullanıcı sorusunu alır  
  - Türkçe, anlaşılır ve kısa cevap üretir  

**Örnek Prompt:**
-Kullanıcı sorusu: "Parol ve Nurofeni aynı anda kullanabilir miyim?"
Veri tabanında bulunan bilgi: "Bu ilaçların birlikte kullanımı mide rahatsızlığı riskini artırabilir."
Talimat: Türkçe, kullanıcı dostu, kısa ve anlaşılır cevap üret.

**Örnek Cevap:**
-Parol ve Nurofen birlikte kullanıldığında bazı kişilerde mide rahatsızlığı görülebilir.
Doktorunuza danışmanız tavsiye edilir.


---

### 4. Frontend (React.js)
- **Özellikler:**  
  - Autocomplete ile ilaç seçme  
  - “Etkileşim Kontrol Et” butonu  
  - Chatbot ekranında AI yanıtları balon formatında gösterme  
  - “Eczacıya sor” opsiyonu  

- **Kullanıcı Akışı:**  
  1. Kullanıcı ilaç isimlerini girer veya yazar  
  2. Backend API çağrılır  
  3. Yanıt chatbot ekranında gösterilir  
  4. İstenirse eczacıya yönlendirilir  

---

### 5. Opsiyonel – Eczacı Entegrasyonu
- İlk sürümde **mock endpoint**:  
  - `/ask_pharmacist` → “Eczacınıza danışın, mesaj gönderildi” cevabı  
- İlerleyen sürümlerde gerçek eczacı entegrasyonu yapılabilir  

---

## ⚡ Kullanıcı Senaryosu (Akış)

1. Kullanıcı → “Parol ve Nurofen aldım, sorun olur mu?”  
2. Backend → NLP ile ilaç isimlerini çıkarır: `[Parol, Nurofen]`  
3. Vector DB → ilgili kaydı bulur  
4. RAG → LLM’e bu bilgiyi verir  
5. LLM → Türkçe yanıt üretir  
6. Frontend → yanıtı chatbot ekranında gösterir  
7. Kullanıcı isterse → “Eczacıya sor” seçeneğini kullanır  

---

## 🚀 Öncelik Sırası (Hackathon için)
1. Veri hazırlığı → CSV temizleme, DB’ye aktarma  
2. Backend prototipi → FastAPI endpoint’leri  
3. Frontend prototipi → React arayüzü (autocomplete + chat)  
4. AI entegrasyonu → NLP + RAG + LLM cevapları  
5. Son rötuşlar → Türkçe cevap kalitesi, UX basitliği  

---

## 👨‍💻 Teknoloji Yığını
- **Frontend:** React.js, Material UI  
- **Backend:** FastAPI (Python)  
- **Database:** SQLite / PostgreSQL + Vector DB (Milvus / FAISS)  
- **AI Katmanı:**  
  - NLP (spaCy, HuggingFace Transformers)  
  - Embedding (Sentence Transformers, OpenAI Embedding)  
  - LLM (Mistral veya benzeri Türkçe destekli model)  

---

## ✨ Özet
Bu proje, **AI destekli ilaç etkileşim kontrol sistemi**dir.  
- Kullanıcı dostu tasarım  
- NLP + RAG + LLM tabanlı güçlü yapay zekâ altyapısı  
- Eczacı entegrasyonu için ölçeklenebilir mimari  

Hackathon için hızlı prototiplenebilir, aynı zamanda gerçek hayatta uygulanabilir bir çözümdür. 🚑💊

