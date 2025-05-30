# Visual Novel Character Name Extractor

A simple web-based tool to quickly extract character names (Japanese and Romaji) and their genders from a visual novel's page on the [Visual Novel Database (VNDB)](https://vndb.org).
The main purpose is to create a prompt for Large Language Model to translate the visual novel.

https://github.com/user-attachments/assets/729cd9df-66ed-44ba-8ca7-7955ed806240

## Description

This tool allows users to input a VNDB visual novel ID or a direct URL to a visual novel page on VNDB. It then fetches data from the VNDB API, including character details and optionally the game's description. The extracted information is displayed in a user-friendly format. The tool also provides options to include a custom template with the output, copy the information to the clipboard, and save it to a text file.

The exported format is  `[Japanese Name] is called [Full Romaji Name]. [Given Name (Romaji)] is [gender].` 

Example: `桜来 瑞花 is called Sakuragi Mizuha. Mizuha is female.`

## Features

* **Flexible Input:** Accepts various VNDB input formats for visual novels:
    * Visual Novel ID (e.g., `16845`)
    * Visual Novel ID with 'v' prefix (e.g., `v16845`)
    * Full Visual Novel URL (e.g., `https://vndb.org/v16845`)
* **Character Information Extraction:**
    * Extracts original Japanese name (or original script name).
    * Extracts Romaji (Latin script) name.
    * Extracts character gender.
* **Game Description Extraction:**
    * Optionally fetches the visual novel's description.
    * Strips BBCode and HTML formatting from the description for cleaner output.
* **Intelligent Name Parsing:** Attempts to identify the given name from the Romaji name for more natural sentence construction in the character list. It considers typical Japanese naming order (Family Given) and Western naming order (Given Family) based on whether the original character name is written entirely in Katakana (often used for Western names in Japanese media).
* **Output Formatting:**
    * Presents extracted character data as: `[Original Name] is called [Full Romaji Name]. [Given Name (Romaji)] is [gender].`
    * If game description is included, it's prepended to the character list.
* **Custom Templates:** Allows users to prepend custom text to the extracted information.
* **Clipboard & File Saving:**
    * "Copy to Clipboard" button for easy sharing.
    * "Save to File" button to download the extracted information as a `.txt` file.
    * Suggests a filename based on the fetched game title (e.g., `[VN_Title]_Characters.txt`).
* **Caching:**
    * Successfully extracted data (including character info, game description, and game title) is cached in the browser's `localStorage` associated with the VNDB ID.
    * Prompts users to load from cache or fetch fresh data if previously extracted data for a VN ID is found. The prompt also considers if the preference for including the game description has changed since the last fetch.
* **Settings Persistence:** Remembers the template content, "include template" checkbox state, "include game description" checkbox state, and the last used filename via `localStorage`.

## How to Use

1.  **Open the `VNCharacterNameExtractor.html` file** in your web browser.
2.  **Enter a VNDB ID or URL** into the input field. Examples:
    * `17`
    * `v17`
    * `https://vndb.org/v17`
3.  **Click the "Extract Character Info" button.**
    * If cached data exists, you'll be asked if you want to load it or fetch new data. This prompt may also appear if your preference for including the game description differs from the cached version.
4.  **(Optional) Check/Uncheck "Include game description"** before extracting to fetch and include the game's story description.
5.  **View the extracted information** in the "Extracted Information" section.
6.  **(Optional) Use Output Options:**
    * Enter text in the "Template" field.
    * Check "Include template in output" to prepend your template to the results.
    * Modify the suggested "Filename" if desired.
    * Click "Copy to Clipboard" or "Save to File".
7.  **(Optional) Save Settings:** Click the "Save Settings" button in the footer to persist your template, checkbox states, and filename for future sessions.

## Technical Details

* **Client-Side Application:** Runs entirely in the user's web browser using HTML, CSS (Tailwind CSS), and JavaScript.
* **VNDB API:** Uses the official VNDB API to fetch visual novel and character data.
    * Visual Novel info (title, description): `https://api.vndb.org/kana/vn`
    * Character info (names, gender): `https://api.vndb.org/kana/character`
* **Local Storage:** Utilizes the browser's `localStorage` for:
    * Caching extracted data (character lists, game descriptions, game titles) to reduce redundant API calls.
    * Persisting user settings (template, filename, checkbox states for template and game description).
* **BBCode/HTML Stripping:** Basic stripping of formatting from game descriptions for cleaner output.

## Disclaimer

* This tool relies on the availability and structure of the official VNDB API. If the API changes, is rate-limited, or becomes unavailable, this tool may not function correctly or at all.
* Always respect VNDB's terms of service when using this tool. It is intended for personal convenience. Be mindful of API request limits.
