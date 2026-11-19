# Hayase Dual Subtitles & Nihongo Helper 🇯🇵

A custom plugin for **Hayase** designed for learning Japanese while watching anime. It intercepts Hayase's internal **JASSUB (`libass` WebAssembly)** worker and **Matroska (`MKV`)** binary subtracks to display synchronized **Japanese, Romaji, English, and Turkish** subtitles simultaneously—complete with an interactive click-to-define dictionary and a torrent subtrack finder.

<img width="1920" height="1079" alt="image" src="https://github.com/user-attachments/assets/209b9a49-b700-43c1-a8ee-da84120c826c" />


---

## Why This Plugin?

Standard browser extensions (such as InterSub, Linglass, or Sublo) do not work inside Hayase for two reasons:
1. **Canvas Rendering:** Hayase renders subtitles directly onto an HTML5 `<canvas>` via JASSUB rather than standard DOM `<track>` elements.
2. **Embedded MKV Subtracks:** Anime releases embed subtitles as binary `S_TEXT/ASS` or `S_TEXT/UTF8` tracks inside the `.mkv` container instead of separate `.srt` files.

This plugin bypasses Electron's isolated content-script boundary, hooks into the `MAIN` execution context, and reads real Matroska `Cluster`/`Block` timestamps directly from the stream so subtitles stay accurately synced—even when seeking or scrubbing through an episode.

<img width="1165" height="294" alt="image" src="https://github.com/user-attachments/assets/f484c6c2-6146-43e7-a803-21c35d0a4b2c" />


---

## Features

- **Multi-Language Stacked Subtitles:** Display **Romaji**, **Japanese (Kanji/Hiragana/Katakana)**, **English**, and **Turkish** translations at the same time.
- **Interactive Click-to-Define Dictionary:** Click any Japanese or English word in the overlay to automatically pause playback and view its Romaji reading alongside Turkish and English translations.
- **MKV Binary Timestamp Extraction:** Parses Matroska `Cluster` + `Block` headers and `JASSUB` cues in real time, preventing subtitle desync or buffer dumping when skipping ahead.
- **Torrent Subtrack Detector & Filter:** Automatically badges releases in Hayase's episode torrent modal (`🟢 JPN + ENG Subtrack`, `🟡 MultiSub`, `🔵 ENG Only`) and adds a one-click filter to find dual-language releases (such as `ToonsHub` / `NF.WEB-DL` MSubs).
- **External Subtitle & Drag-and-Drop Support:** Load or drag-and-drop external `.srt`, `.ass`, `.ssa`, or `.vtt` files directly onto the player (with a quick link to [Jimaku.cc](https://jimaku.cc) for Japanese scripts).
- **Live Sync & Layout Controls:** Fine-tune subtitle timing (`-1s`, `-0.2s`, `0`, `+0.2s`, `+1s`) and toggle overlay position between the top and bottom of the screen.

<img width="388" height="826" alt="image" src="https://github.com/user-attachments/assets/0d1124ea-b5f4-496c-8aa2-c496d287703b" />


---

## Project Structure

```text
hayase-dual-sub/
├── manifest.json   # Manifest V3 configuration & web accessible resources
├── injector.js     # Bypasses Electron isolated world to inject page.js into MAIN context
└── page.js         # MKV/JASSUB hooks, torrent filter UI, subtitle renderer & dictionary
```

---

## Installation

1. Clone or download this repository to a local folder (e.g., `hayase-dual-sub`):
   ```bash
   git clone [https://github.com/](https://github.com/)<your-username>/hayase-dual-sub.git
   ```
2. Open **Hayase** and navigate to **Settings → Plugins**.
3. Click **Install Plugin**.
4. Browse to the `hayase-dual-sub` folder and select **`manifest.json`**.
5. Ensure the plugin is toggled **ON**, then reload Hayase (`Ctrl + R` or restart the app).

---

## Usage

1. **Choose a Release with Japanese Subtracks:**
   - When selecting an episode torrent, use the **Subtrack Filter** bar to filter for **`🟢 JPN + ENG`** releases (e.g., `ToonsHub` / Netflix `MSubs` rips), or download a Japanese `.ass`/`.srt` file from **Jimaku.cc**.
2. **Activate the Subtitle Track:**
   - Start playback, open Hayase's native **Subtitles** menu, and select **`Jpn`**.
   - The plugin will capture the timestamped Japanese lines and render Romaji, Japanese, English, and Turkish in the overlay.
3. **Customize via the Control Panel:**
   - Click the **`🇯🇵 Çift Altyazı`** button in the top-right corner of the video player to switch primary/secondary tracks, toggle Romaji or Turkish translation, load external subtitle files, or adjust sync offset.

---

## License

MIT License. Free to use, modify, and distribute.
