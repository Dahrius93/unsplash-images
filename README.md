# 🖼️ Unsplash Images

Un'applicazione React moderna per cercare e visualizzare immagini dalla libreria Unsplash.

## 📋 Descrizione

**Unsplash Images** è un'applicazione web intuitiva che permette di cercare e visualizzare immagini di alta qualità direttamente dall'API di Unsplash. L'app offre un'interfaccia pulita con supporto per il tema chiaro e scuro.

### ✨ Caratteristiche Principali

- **🔍 Ricerca Immagini**: Ricerca in tempo reale di immagini tramite l'API Unsplash
- **🎨 Tema Scuro/Chiaro**: Toggle per passare tra tema chiaro e scuro
- **⚡ Caricamento Ottimizzato**: Caching intelligente con React Query
- **📱 Responsive Design**: Perfetto su dispositivi desktop e mobile
- **🚀 Performante**: Costruito con Vite per velocità massima

## 🛠️ Tecnologie Utilizzate

- **React 18.2** - Libreria UI
- **Vite** - Build tool e dev server
- **React Query (TanStack)** - Gestione del caching e dello stato asincrono
- **Axios** - Client HTTP
- **React Icons** - Libreria di icone
- **CSS** - Styling (responsive)

## 📦 Installazione

### Prerequisiti

- Node.js (versione 14 o superiore)
- npm o yarn

### Setup del Progetto

1. **Clona il repository**
   ```bash
   git clone <repository-url>
   cd unsplash-images
   ```

2. **Installa le dipendenze**
   ```bash
   npm install
   ```

3. **Configura le variabili d'ambiente**
   
   Crea un file `.env` nella root del progetto:
   ```
   VITE_API_KEY=your_unsplash_api_key_here
   ```
   
   > 📝 Ottieni una chiave API gratuita [qui](https://unsplash.com/developers)

4. **Avvia il server di sviluppo**
   ```bash
   npm run dev
   ```
   
   L'applicazione si aprirà automaticamente a `http://localhost:5173`

## 🚀 Utilizzo

### Ricerca Immagini

1. Inserisci il termine di ricerca nell'input (es. "cat", "mountain", "nature")
2. Clicca il pulsante **Search** o premi Enter
3. Le immagini verranno caricate e visualizzate nella galleria

### Toggle Tema

Clicca l'icona nella barra superiore per passare tra tema chiaro e scuro. La preferenza viene salvata automaticamente.

### Gestione Errori

- **Loading**: Viene visualizzato "Loading..." durante il caricamento
- **Errori**: In caso di errore API viene mostrato un messaggio di errore

## 📁 Struttura del Progetto

```
unsplash-images/
├── src/
│   ├── App.jsx              # Componente principale
│   ├── context.jsx          # Context globale (search term, tema)
│   ├── SearchForm.jsx       # Form di ricerca
│   ├── Gallery.jsx          # Galleria di immagini
│   ├── ThemeToggle.jsx      # Toggle tema scuro/chiaro
│   ├── main.jsx             # Entry point React
│   ├── index.css            # Stili globali
│   └── assets/              # Risorse statiche
├── public/                  # File statici
├── .env                     # Configurazione (non committare)
├── vite.config.js           # Configurazione Vite
├── package.json             # Dipendenze e script
└── README.md               # Questo file
```

### Componenti

#### `App.jsx`
Componente radice che orchestra i principali componenti dell'app.

#### `SearchForm.jsx`
Form di ricerca che cattura l'input dell'utente e aggiorna il contesto globale.

#### `Gallery.jsx`
Componente che esegue la query all'API Unsplash e visualizza le immagini. Gestisce loading e errori.

#### `ThemeToggle.jsx`
Pulsante per alternare tra tema chiaro e scuro.

#### `context.jsx`
Context React per lo stato globale:
- `searchTerm`: Termine di ricerca corrente
- `setSearchTerm`: Funzione per aggiornare il termine
- `theme`: Tema corrente (light/dark)
- `toggleTheme`: Funzione per cambiare tema

## 📜 Script Disponibili

```bash
# Avvia il server di sviluppo
npm run dev

# Build per la produzione
npm run build

# Preview della build di produzione
npm run preview
```

## 🌐 API Reference

L'app utilizza l'**Unsplash API** (`https://api.unsplash.com/search/photos`)

### Parametri
- `client_id`: Chiave API Unsplash (da .env)
- `query`: Termine di ricerca

### Risposta
Restituisce array di oggetti immagine con:
- `id`: ID immagine
- `urls`: Oggetto con vari formati URL
- `alt_description`: Descrizione alternativa

[Documentazione Unsplash API](https://unsplash.com/documentation)

## 🎨 Personalizzazione

### Cambiare i colori del tema

Modifica i CSS custom in `index.css`:

```css
:root {
  --background-color: #ffffff;
  --text-color: #000000;
  /* ... altri colori */
}

[data-theme="dark"] {
  --background-color: #1a1a1a;
  --text-color: #ffffff;
}
```

### Aggiungere filtri di ricerca

Estendi `Gallery.jsx` con parametri aggiuntivi:

```javascript
const response = useQuery({
  queryFn: async () => {
    const result = await axios.get(
      `${URL}&query=${searchTerm}&per_page=20&order_by=relevant`
    );
    return result.data;
  },
});
```

## ⚠️ Limitazioni API

La versione gratuita di Unsplash API ha i seguenti limiti:
- 50 richieste per ora (non autenticato)
- 5000 richieste al giorno

## 🐛 Troubleshooting

### Immagini non si caricano
- Verifica che `VITE_API_KEY` è correttamente impostato nel file `.env`
- Controlla che la chiave API è valida
- Verifica la connessione a internet

### Errore "Too many requests"
- Aspetta un'ora prima di fare nuove ricerche
- Considera di autenticarti con Unsplash per limiti maggiori

### Build fallisce
```bash
# Pulisci la cache e reinstalla
rm -rf node_modules package-lock.json
npm install
npm run build
```

## 📝 Note di Sviluppo

- React Query gestisce automaticamente il caching - le stesse ricerche non faranno nuove richieste API
- Il tema viene mantenuto in localStorage per persistenza tra sessioni
- Vite utilizza ES modules per caricamento più veloce in sviluppo

## 🚀 Deploy

### Vercel (Consigliato)

```bash
npm install -g vercel
vercel
```

Aggiungi le variabili d'ambiente in Vercel Dashboard:
- `VITE_API_KEY`: Tua chiave API Unsplash

### Netlify

1. Connetti il repository a Netlify
2. Build command: `npm run build`
3. Publish directory: `dist`
4. Aggiungi `VITE_API_KEY` nelle variabili d'ambiente

### Build locale

```bash
npm run build
# La cartella 'dist' contiene i file pronti per il deploy
```

## 📚 Risorse Utili

- [React Documentation](https://react.dev)
- [Vite Guide](https://vitejs.dev)
- [React Query Docs](https://tanstack.com/query/latest)
- [Unsplash API](https://unsplash.com/documentation)
- [Axios Documentation](https://axios-http.com)

## 📄 Licenza

Questo progetto è disponibile sotto licenza MIT.

## 👨‍💻 Autore

Creato durante il corso Udemy di React.

---

**Buon divertimento con Unsplash Images!** ✨
