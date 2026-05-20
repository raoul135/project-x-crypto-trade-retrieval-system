# 🔐 DPIA — Project-X Crypto Trade Retrieval System

> **Data Protection Impact Assessment (DPIA)**
> GDPR-conforme AI & Retrieval Architectuur
> Project-X — Lokale AI Trade Intelligence & Retrieval Platform

---

# 📖 1. Inleiding

Dit document beschrijft de volledige GDPR-conforme architectuur en privacy-implementatie van het **Project-X Crypto Trade Retrieval System**.

Project-X is een lokaal draaiend **Retrieval-Augmented Generation (RAG)** systeem dat ontworpen werd voor het analyseren, vergelijken en evalueren van historische cryptocurrency trades via:

* semantische vector embeddings
* retrieval workflows
* lokale AI verwerking
* workflow orchestratie
* retrieval evaluatie

Het systeem combineert:

* 📊 gestructureerde trade data
* 🧠 semantische embeddings
* 🔍 vector retrieval
* 🐳 lokale Docker infrastructuur
* ⚙️ workflow orchestratie via n8n
* 🤖 lokale AI verwerking via LM Studio

---

# 🏗️ 2. Systeemoverzicht

Het systeem bestaat uit meerdere logisch gescheiden componenten:

| Component          | Functie                           | GDPR-impact               |
| ------------------ | --------------------------------- | ------------------------- |
| ⚙️ n8n Workflows   | Workflow orchestratie + validatie | Controle & audit logging  |
| 🧠 LM Studio       | Lokale embedding generatie        | Geen externe data sharing |
| 🗄️ Qdrant         | Vector database & retrieval       | Geen directe PII opslag   |
| 🐘 PostgreSQL      | Marktdata & historische metrics   | Lokale opslag             |
| 📋 n8n Data Tables | PII opslag + audit logging        | Volledig controleerbaar   |

---

# 🧾 3. Data Classificatie

## 📊 3.1 Niet-persoonlijke Trade Data

De volgende data wordt gebruikt voor embeddings en retrieval:

| Veld                  | Beschrijving      |
| --------------------- | ----------------- |
| `pair`                | BTCUSDT / ETHUSDT |
| `position_side`       | LONG / SHORT      |
| `strategy`            | Trading strategie |
| `trend_direction`     | Markttrend        |
| `volatility_category` | Volatiliteit      |
| `market_pressure`     | Marktcondities    |
| `rsi_category`        | RSI classificatie |
| `sentiment_state`     | Marktsentiment    |

✅ Deze data bevat **geen direct identificeerbare persoonsgegevens**

---

## 👤 3.2 Persoonsgegevens (PII)

De volgende data wordt beschouwd als gevoelige informatie:

| Veld             | Beschrijving            |
| ---------------- | ----------------------- |
| `user_id`        | Interne identifier      |
| `email`          | Contactinformatie       |
| `wallet_address` | Blockchain wallet adres |

---

## ❗ Belangrijk Privacy Principe

> Deze velden worden **NOOIT** opgenomen in embeddings of opgeslagen in Qdrant collections.

---

# 🛡️ 4. Kernprincipes van de Architectuur

Het systeem werd ontworpen volgens drie fundamentele GDPR-principes.

---

## 🔒 4.1 Privacy by Design

PII wordt vanaf het begin van de ingestion pipeline logisch en fysiek gescheiden van AI-verwerking en retrieval workflows.

---

## 📉 4.2 Data Minimalisatie

Alleen strikt noodzakelijke markt- en trade-context data wordt gebruikt voor embeddings en retrieval.

---

## 🧩 4.3 Separation of Concerns

PII opslag, embeddings, retrieval en audit logging zijn volledig gescheiden componenten binnen de architectuur.

---

# 🔄 5. Data Flow Overzicht

De verwerking binnen het systeem verloopt als volgt:

1. 📥 Trade data wordt ingestuurd via intake workflow
2. ⚙️ Coordinator workflow valideert de input
3. 👤 PII wordt apart opgeslagen
4. 📊 Markt- en sentimentverrijking wordt uitgevoerd
5. 🧠 Embeddings worden lokaal gegenereerd via LM Studio
6. 🗄️ Vectoren worden opgeslagen in Qdrant
7. 📋 Audit logs registreren elke stap
8. 🔍 Retrieval workflows gebruiken enkel niet-PII data

---

## ✅ Resultaat

Deze architectuur maakt het systeem:

* controleerbaar
* auditbaar
* transparant
* GDPR-conscious
* reproduceerbaar

---

# ⚠️ 6. Risicoanalyse

## 📉 6.1 Risicoanalyse vóór mitigatie

| Risico                           | Probability | Severity | Uitleg                           |
| -------------------------------- | ----------- | -------- | -------------------------------- |
| Ongeautoriseerde toegang tot PII | Medium      | High     | PII bevat gevoelige data         |
| Embedding leakage                | Low         | High     | Mogelijke indirecte info leakage |
| Onvolledige verwijdering         | Medium      | Medium   | Data verspreid over systemen     |

---

## 🛡️ 6.2 Mitigatie na implementatie

| Risico            | Mitigatie                     | Remaining Risk |
| ----------------- | ----------------------------- | -------------- |
| PII toegang       | Data separation               | Low            |
| Embedding leakage | Geen PII embeddings           | Very Low       |
| Deletion issues   | Metadata delete + verificatie | Low            |

---

# 🔐 7. Mitigerende Maatregelen

## 🧩 7.1 Data Separation

PII wordt volledig gescheiden opgeslagen van embeddings en retrieval data.

---

## 🐳 7.2 Lokale Deployment

Alle componenten draaien lokaal via:

* Docker
* n8n
* LM Studio
* PostgreSQL
* Qdrant

Dit betekent:

* ❌ geen externe inference APIs
* ❌ geen cloud vector databases
* ❌ geen third-party data sharing
* ✅ volledige controle over data

---

## 📉 7.3 Data Minimalisatie

Embeddings bevatten enkel:

* marktdata
* technische indicatoren
* contextuele trade informatie

Niet opgenomen:

* email adressen
* wallet adressen
* user identifiers

---

# 🗑️ 8. Artikel 17 — Recht op Vergetelheid

Het systeem ondersteunt GDPR Artikel 17 via een gestructureerde delete-procedure.

---

## 🧹 Stap 1 — Verwijderen van PII

PII wordt verwijderd uit n8n Data Tables.

---

## 🗄️ Stap 2 — Verwijderen van Vector Data

Gerelateerde Qdrant vectors worden verwijderd via metadata filtering.

---

## ✅ Stap 3 — Verificatie

Het systeem controleert:

* query geeft geen resultaten meer terug
* vector bestaat niet meer
* audit logs bevestigen delete operatie

---

# 🔍 9. Source Attribution & Traceability

Elke retrieval output kan gekoppeld worden aan:

* `trade_id`
* `chunk_id`
* workflow source
* retrieval context

Dit ondersteunt:

* transparantie
* traceability
* auditability
* gerichte verwijdering

---

# 🏛️ 10. Privacy Architectuur

Het systeem gebruikt bewust een **local-first AI architectuur**.

| Factor            | Cloud Architectuur | Project-X     |
| ----------------- | ------------------ | ------------- |
| Data Controle     | Beperkt            | Volledig      |
| Data Sharing      | Mogelijk           | Niet aanwezig |
| Privacy Risico    | Hoger              | Lager         |
| GDPR Complexiteit | Hoog               | Lager         |

---

# 📋 11. Audit Logging

Het systeem registreert:

* workflow execution
* validatie fouten
* retrieval acties
* delete operaties
* verwerking status

---

## 📑 Audit Log Velden

| Veld              | Beschrijving        |
| ----------------- | ------------------- |
| `createdAt`       | Tijdstip verwerking |
| `trade_id`        | Trade identifier    |
| `workflow_source` | Workflow oorsprong  |
| `action`          | Type verwerking     |
| `result`          | Success / Failure   |

---

# 🧠 12. AI Transparantie

Alle AI-output binnen het systeem wordt expliciet behandeld als:

> “AI-generated analysis”

Hierdoor blijft duidelijk onderscheid bestaan tussen:

* menselijke interpretatie
* AI-gegenereerde analyse

Dit ondersteunt AI Act transparantieprincipes.

---

# ✅ 13. Conclusie

Het **Project-X Crypto Trade Retrieval System** vormt een GDPR-conforme implementatie van een moderne lokale AI retrieval architectuur.

De combinatie van:

* 🔒 data separation
* 📉 data minimalisatie
* 🧠 lokale AI verwerking
* 🔍 retrieval traceability
* 📋 audit logging
* 🗑️ controleerbare delete procedures
* 🐳 lokale infrastructuur

zorgt ervoor dat het systeem:

* veilig
* controleerbaar
* reproduceerbaar
* transparant
* GDPR-conscious

kan worden beschouwd.

---

# 🏁 Eindconclusie

> Project-X werd ontworpen volgens een **Privacy by Design** filosofie waarbij controle, transparantie en minimale blootstelling van persoonsgegevens centraal staan.
