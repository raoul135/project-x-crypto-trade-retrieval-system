# 🚀 Project-X Crypto Trade Retrieval System

## 📖 Overzicht

Project-X is een lokaal AI-assisted retrieval platform ontworpen voor het analyseren, vergelijken en contextualiseren van historische cryptocurrency trades.

Het systeem combineert:

- 🔄 Workflow automatisatie  
- 🧠 Lokale AI verwerking  
- 🔍 Vector embeddings  
- 📊 Semantische retrieval  

om historische trade setups sneller, consistenter en schaalbaarder analyseerbaar te maken.

---
# 📁 Repository Structuur

```text
VOORNAAM_ACHTERNAAM_Eindproject/
│
├── README.md
│
├── workflows/
│   ├── Project-X Coordinator Workflow.json
│   ├── Project-X Trade Ingestion Workflow.json
│   ├── Project-X Market Feature Extraction.json
│   ├── Project-X News Sentiment Extraction.json
│   ├── Project-X Trade Retrieval Evaluation.json
│   └── Project-X Trade Close Update.json
│
├── screenshots/
│   ├── docker/
│   ├── n8n/
│   ├── lm-studio/
│   └── demo-screenshots/
│
├── documentation/
│   ├── architecture-diagram/
│   └── dpia/
│
├── database/
│   └── market_data_sample.sql
│
├── business-case/
│   ├── roi-analysis.xlsx
│   └── leidinggevende-1pager.pdf
│
└── Trade Input.html
```

# ⚙️ Setup (Docker Desktop GUI)

## 📋 Stap 1: Vereisten

Voor het uitvoeren van het systeem zijn volgende componenten vereist:

- 🐳 Docker Desktop geïnstalleerd
- 🧠 LM Studio geïnstalleerd
- 📂 GitHub repository gedownload
- 💻 Windows 10/11 aanbevolen

---

# 🐳 Stap 2: Containers starten

## 🔄 n8n

1. Open Docker Desktop → `Images`
2. Zoek: `n8nio/n8n`
3. Klik `Pull`
4. Klik `Run`

### Configuratie

| Setting | Waarde |
|---|---|
| Name | `x-n8n` |
| Port | `5678:5678` |
| Volume | `x-n8n-data` |

5. Start container
6. Controleer:
   http://localhost:5678

---

## 🔎 Qdrant

1. Open Docker Desktop → `Images`
2. Zoek: `qdrant/qdrant`
3. Klik `Pull`
4. Klik `Run`

### Configuratie

| Setting | Waarde |
|---|---|
| Name | `x-qdrant` |
| Port | `6333:6333` |
| Volume | `x-qdrant-data` |

5. Start container
6. Controleer:
   http://localhost:6333/dashboard

---

## 🗄️ PostgreSQL

1. Open Docker Desktop → `Images`
2. Zoek: `postgres`
3. Klik `Pull`
4. Klik `Run`

### Configuratie

| Setting | Waarde |
|---|---|
| Name | `x-postgres` |
| Port | `5432:5432` |

### Environment Variables

```env
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
```

### Volume

```text
x-postgres-data
```

5. Start container

---

# 🧠 Stap 3: LM Studio Configuratie

1. Open LM Studio

2. Download / laad de volgende modellen:

| Model | Functie |
|---|---|
| `text-embedding-bge-m3` | Embedding generatie & vector search |
| `llama-3.2-3b-instruct` | Lokale AI-analyse & evaluatie-output |

3. Start de LM Studio Local Server

4. Controleer:
   http://localhost:1234

---

# 🗄️ Stap 4: Database Import

1. Open PostgreSQL of pgAdmin
2. Maak database:
   `Final-Project-Raoul`

3. Importeer:

```text
/database/market_data_sample.sql
```

4. Controleer of volgende tabellen bestaan:

- `coin_metrics`
- `coins`
- `crypto_prices`

---

# 🔄 Stap 5: Workflows importeren

1. Open n8n
2. Klik `Import Workflow`
3. Selecteer de JSON-bestanden uit `/workflows/`
4. Importeer alle workflows
5. Controleer of alle nodes correct geladen zijn
6. Stel credentials en connecties in indien nodig

---

# 🧪 Stap 6: Testen

## ✅ Test 1 — Workflow Trigger

1. Open de Coordinator Workflow
2. Activeer de webhook
3. Open `/Trade Input.html`
4. Vul een test trade in
5. Klik `Submit Trade`
6. Controleer succesvolle workflow execution in n8n

---

## 🧠 Test 2 — Embedding Generatie

1. Controleer of LM Studio actief is
2. Run de Trade Ingestion Workflow
3. Controleer succesvolle embedding generatie

---

## 🔍 Test 3 — Qdrant Storage

1. Open Qdrant Dashboard
2. Controleer collections
3. Controleer nieuwe vector insertions

---

## 📊 Test 4 — Retrieval Workflow

1. Open de Retrieval Workflow
2. Voer retrieval query uit
3. Controleer retrieval resultaten en similarity scores

---

# 🏗️ Architectuur

![Project Architecture](documentation/architecture-diagram/architecture-diagram.png)

Project-X gebruikt een lokaal retrieval-gebaseerd AI-platform waarbij trades eerst gevalideerd en verrijkt worden via n8n workflows. Daarna worden embeddings lokaal gegenereerd via LM Studio en opgeslagen in Qdrant.

De retrieval workflows gebruiken semantische vector search en metadata filtering om vergelijkbare historische trades terug te vinden.

## 🔧 Belangrijkste componenten

- 🔄 n8n → workflow orchestratie
- 🧠 LM Studio → lokale embeddings & AI verwerking
- 🗄️ PostgreSQL → marktdata opslag
- 🔎 Qdrant → vector retrieval database
- 🐳 Docker → lokale infrastructuur

---

# 🎥 Demo Video

📎 Voeg hier demo video link toe.

---