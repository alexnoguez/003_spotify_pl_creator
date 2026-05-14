# SpotifyPy

A personal web app that generates Spotify playlists from a list of artists. Paste up to 50 artist names, configure how many top tracks to pull per artist (globally or individually), name your playlist, and hit generate — a new playlist lands in your Spotify account instantly.

---

## Features

- Paste up to **50 artists** at once, one per line
- Set a **global track count** (1–20) and override it **per artist** individually
- Optional custom playlist name (auto-generated from artist names if left blank)
- Tracks are ranked by **popularity** on Spotify (US market)
- Results show a full breakdown of which artists were found and how many tracks were added
- Matrix-themed UI with animated equalizer and canvas rain effect

---

## How It Works

1. The Flask backend receives a list of artists and their track counts from the browser
2. For each artist it searches the Spotify API to resolve the canonical artist ID
3. It then fetches up to 50 of their tracks, filters to confirmed matches, and sorts by popularity
4. A new public playlist is created on your Spotify account and all tracks are added in one pass

**Stack:** Python · Flask · [Spotipy](https://spotipy.readthedocs.io/) · vanilla HTML/CSS/JS

---

## Prerequisites

- Python 3.10+
- A [Spotify Developer](https://developer.spotify.com/dashboard) account and app

---

## Setup

### 1. Clone the repo

```bash
git clone https://github.com/your-username/SpotifyPy.git
cd SpotifyPy
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Create a Spotify Developer app

1. Go to [developer.spotify.com/dashboard](https://developer.spotify.com/dashboard) and log in
2. Click **Create App**
3. Fill in any name and description
4. Under **Redirect URIs**, add: `http://127.0.0.1:8888/callback`
5. Save and copy your **Client ID** and **Client Secret**

### 4. Configure environment variables

Create a `.env` file in the project root:

```env
SPOTIFY_CLIENT_ID=your_client_id_here
SPOTIFY_CLIENT_SECRET=your_client_secret_here
SPOTIFY_REDIRECT_URI=http://127.0.0.1:8888/callback
```

> `.env` is listed in `.gitignore` and will never be committed.

### 5. Authenticate (first run only)

The first time you run the app, Spotipy will open a browser window asking you to authorize the app against your Spotify account. After you approve, it caches the token in a `.cache` file locally so you won't be prompted again.

### 6. Run

```bash
python app.py
```

Open [http://localhost:5000](http://localhost:5000) in your browser.

---

## Project Structure

```
SpotifyPy/
├── app.py              # Flask server + Spotify API logic
├── spotify_client.py   # OAuth client setup
├── main.py             # Original CLI version (optional)
├── artists.txt         # Default artist list (pre-fills the UI)
├── templates/
│   └── index.html      # Web interface
├── requirements.txt
├── .env                # Your credentials — never commit this
└── .gitignore
```

---

## Customizing the Default Artist List

Edit `artists.txt` (one artist per line) to pre-fill the textarea on load. The file is committed to the repo so it serves as a starting point — overwrite it with your own artists.

---

## API Scopes Used

| Scope | Reason |
|---|---|
| `playlist-modify-public` | Create and populate public playlists |
| `playlist-modify-private` | Create and populate private playlists |

---

## License

MIT
