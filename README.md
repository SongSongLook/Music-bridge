# Apple Music/Spotify music bridge for macOS
it is a lightweight desktop application that plays every track through Apple Music’s high-fidelity player while outsourcing “Up Next” song selection to Spotify’s class-leading recommendation engine. The result is an uninterrupted listening session where you enjoy Apple Music’s sound quality and Spotify’s discovery magic.

```
am-spotify-music-bridge/
├─ .env.example         
├─ package.json
├─ vite.config.mjs     
├─ electron.config.js    
├─ main/                
│  ├─ index.js
│  ├─ preload.js
│  └─ services/
│     ├─ spotify.js
│     ├─ apple.js
│     ├─ cache.js
│     └─ mapper.js
└─ renderer/            
   ├─ index.html
   ├─ main.jsx
   └─ components/
      ├─ SearchBar.jsx
      ├─ Queue.jsx
      ├─ NowPlaying.jsx
      └─ Controls.jsx

```

## Functional Workflow – “Apple Music × Spotify Recommendations”

```mermaid
graph TD
    A["User selects first Apple Music track"] -->|Apple&nbsp;ID| B["MusicKit JS player"]
    B -->|When playback time &lt; 30 s| C["Read current track metadata\n(ISRC / title / artist)"]
    C --> D["Spotify Search -> current track ID"]
    D --> E["Spotify Get Recommendations\n(seed = current track ID)"]
    E --> F["Apple Music Catalog Search\n(title + artist) -> Apple track ID"]
    F --> G["music.queue.append(nextAppleTrackId)"]
    G --> H["Next song plays seamlessly\nin Apple Music"]
