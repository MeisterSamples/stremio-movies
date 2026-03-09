# Stremio Movie Catalog from Google Sheets

This repository hosts a simple custom add-on for **Stremio** that displays a personal movie catalog. The catalog data is generated from a Google Sheet and served through GitHub Pages.

The add-on allows you to maintain a list of movies in a spreadsheet and automatically expose them as a catalog inside Stremio.

---

## How It Works

The system consists of three parts:

1. **Google Sheet**
   Stores the movie list.

2. **Google Apps Script**

   * Automatically fetches IMDb IDs using the TMDb API.
   * Generates catalog JSON.

3. **GitHub Pages (this repository)**
   Hosts the static files that Stremio loads.

Workflow:

```
Google Sheet
↓
Apps Script generates JSON
↓
JSON pushed or copied into this repository
↓
GitHub Pages hosts the files
↓
Stremio loads the catalog
```

---

## Repository Structure

```
stremio-movies
│
├ manifest.json
│
└ catalog
   └ movie
      └ sheetmovies.json
```

### manifest.json

Defines the add-on configuration that Stremio loads first.

### catalog/movie/sheetmovies.json

Contains the list of movie metadata entries (IMDb IDs and titles).

Stremio automatically retrieves posters, descriptions, and other metadata using the IMDb ID.

---

## Installing the Add-on in Stremio

Install the add-on using the manifest URL:

```
https://YOURUSERNAME.github.io/stremio-movies/manifest.json
```

Steps:

1. Open Stremio
2. Go to **Add-ons**
3. Click **Install via URL**
4. Paste the manifest URL above

The catalog will then appear inside Stremio as:

```
My Movies
```

---

## Example Catalog Entry

```
{
  "metas": [
    {
      "id": "tt0816692",
      "type": "movie",
      "name": "Interstellar"
    }
  ]
}
```

Only the IMDb ID is required. Stremio retrieves all additional metadata automatically.

---

## Spreadsheet Format

The Google Sheet used to generate the catalog typically looks like this:

| Title             | Year | IMDb      | Category |
| ----------------- | ---- | --------- | -------- |
| Interstellar      | 2014 | tt0816692 | Sci-Fi   |
| Blade Runner 2049 | 2017 | tt1856101 | Sci-Fi   |

The Apps Script can automatically fill the **IMDb column** using the TMDb API.

---

## Future Improvements

Possible enhancements include:

* Automatic GitHub updates from Apps Script
* Multiple catalog rows (categories)
* Poster image support
* Automatic metadata enrichment

---

## Disclaimer

This repository only provides catalog metadata.
It does **not host or distribute media files**.
