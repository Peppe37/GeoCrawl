# Progetto: GeoCollector App 🌍
## Manuale di Definizione Progetto

## Indice

[__TOC__]

### Visione del Prodotto
L'applicazione è un "atlante personale delle esperienze". Permette agli utenti di creare mappe tematiche (es. baci, viaggi, cibo) che tracciano eventi geografici. Il sistema scala automaticamente la visualizzazione e le statistiche da livello locale (città) a globale (continenti).

### Stack Tecnologico Consigliato
* **Frontend:** React 19 + TypeScript + Vite.
* **Styling:** Tailwind CSS.
* **Mappe:** Leaflet.js con OpenStreetMap (React-Leaflet).
* **Backend:** Python 3.11+ con **FastAPI** (scelto per velocità e gestione asincrona).
* **Database:** **SQLite3** (semplice, file-based, perfetto per lo sviluppo iniziale).
* **ORM:** SQLModel (unisce Pydantic e SQLAlchemy per Python).

### Architettura del Database (Schema)

| Tabella | Descrizione |
| :--- | :--- |
| **Users** | ID, Username, Email, Password Hash, Totale Badge. |
| **Maps** | ID, Nome (es. "Kiss Map"), Tipo (Collaborativa/Competitiva), CreatoreID. |
| **Points** | ID, MapID, UserID, Latitudine, Longitudine, Città, Regione, Nazione, Continente, Timestamp. |
| **MapParticipants** | MapID, UserID, Ruolo (Proprietario/Collaboratore), ColoreAssegnato. |
| **Achievements** | ID, UserID, Tipo (Città/Nazioni/Continenti), Livello raggiunto (Fibonacci). |

### Caratteristiche Principali

#### Mapping e Scaling Automatico
L'utente inserisce un punto sulla mappa. Il sistema esegue una **Reverse Geocoding API** per determinare e salvare:
1.  Città
1.  Regione / Provincia
1.  Nazione
1.  Continente
Questo permette di scalare le visualizzazioni (es. "Vedi tutti i baci in Europa").

#### Gamification: Sistema Fibonacci
Gli obiettivi (Achievement) si sbloccano seguendo la sequenza di Fibonacci: **1, 2, 3, 5, 8, 13, 21...**
* **Logica:** Se hai baciato in 5 città diverse, sblocchi l'obiettivo "Viaggiatore".
* **Badge:** Ogni *n* obiettivi raggiunti (es. ogni 3), l'utente riceve un Badge grafico nel profilo.

#### Mappe Condivise
* **Modalità Collaborativa (es. Fidanzati):** Due o più utenti scrivono sulla stessa mappa. I progressi e le statistiche sono condivisi e unificati.
* **Modalità Competitiva (es. Amici):** Gli utenti condividono la visuale, ma ognuno ha un colore diverso. Il sistema genera una classifica basata su chi ha "conquistato" più città o nazioni.

### Roadmap di Sviluppo

1.  **Fase 1 (MVP):** Setup FastAPI + SQLite. Login utente e creazione della prima mappa con inserimento punti manuale (Lat/Lng).
1.  **Fase 2 (Geocoding):** Integrazione API esterne per mappare automaticamente città e nazioni partendo dalle coordinate.
1.  **Fase 3 (Social):** Sistema di inviti per collaboratori e gestione dei colori diversi nella modalità competitiva.
1.  **Fase 4 (Achievements):** Implementazione della logica matematica di Fibonacci per lo sblocco dei badge.
