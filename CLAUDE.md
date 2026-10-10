# Regole di progetto — elixir-ui

## ActiveCampaign: mai creare liste né iscrivere contatti senza autorizzazione (REGOLA FERREA)

- **Non creare mai una lista nuova su ActiveCampaign** e **non iscrivere mai contatti a una lista AC** — da script, API, MCP, import CSV o codice dell'app — senza l'**autorizzazione esplicita** dell'utente per quell'operazione.
- **Prima** di chiedere l'autorizzazione, dare un **allerta preventivo** chiaro: quale lista, quanti contatti, e quali automazioni collegate possono partire.
- Perché: l'iscrizione a una lista fa partire le **automazioni AC** e il **bot scrive ai contatti** (email, SMS, WhatsApp, chiamate). Un'iscrizione sbagliata manda messaggi veri a persone vere e non si può annullare.
- Stessa cautela per le operazioni che possono innescare automazioni: aggiungere tag, creare o aggiornare contatti (`contact/sync`). Il 10/10/2026 un sync di 104 contatti ne ha fatti entrare 13 nell'automazione 62.
- L'autorizzazione vale solo per quell'operazione: non si estende ad altre liste, altri contatti o altri giorni. In dubbio, fermarsi e chiedere.
