# Visual Novel Character Name Extractor

A simple web-based tool to quickly extract character names (Japanese and Romaji) and their genders from a visual novel's page on the [Visual Novel Database (VNDB)](https://vndb.org).
The main purpose is to create a prompt for Large Language Model to translate the visual novel but you can use the information however you want.

https://github.com/user-attachments/assets/729cd9df-66ed-44ba-8ca7-7955ed806240

## Description

This tool allows users to input a VNDB visual novel ID, a direct URL to a visual novel page, or a character page URL on VNDB. It then fetches the page content (via a CORS proxy), parses the HTML to find character details, and displays the extracted information in a user-friendly format. The tool also provides options to include a custom template with the output, copy the information to the clipboard, and save it to a text file.

The exported format is  `[Japanese Name] is called [Full Romaji Name]. [Given Name (Romaji)] is [gender].` 

Example: `桜来 瑞花 is called Sakuragi Mizuha. Mizuha is female.`

## Features

* **Flexible Input:** Accepts various VNDB input formats:
    * Visual Novel ID (e.g., `16845`)
    * Visual Novel ID with 'v' prefix (e.g., `v16845`)
    * Full Visual Novel URL (e.g., `https://vndb.org/v16845`)
    * Direct Character Page URL (e.g., `https://vndb.org/v16845/chars` or `https://vndb.org/c1234`)
* **Automatic URL Correction:** If a base VN URL (like `/vXXXXX`) is provided, `/chars` is automatically appended to target the character list page.
* **Character Information Extraction:**
    * Extracts original Japanese name.
    * Extracts Romaji (Latin script) name.
    * Extracts character gender.
* **Intelligent Name Parsing:** Attempts to identify the given name from the Romaji name for more natural sentence construction, considering typical Japanese and Western naming conventions based on the script used in the original Japanese name.
* **Output Formatting:** Presents extracted data as:
    `[Japanese Name] is called [Full Romaji Name]. [Given Name (Romaji)] is [gender].`
* **Custom Templates:** Allows users to prepend custom text to the extracted information.
* **Clipboard & File Saving:**
    * "Copy to Clipboard" button for easy sharing.
    * "Save to File" button to download the extracted information as a `.txt` file.
    * Suggests a filename based on the extracted game title.
* **Caching:**
    * Successfully extracted data is cached in the browser's `localStorage` associated with the VNDB ID.
    * Prompts users to load from cache or fetch fresh data if previously extracted data for a URL/ID is found.
* **Settings Persistence:** Remembers the template content, "include template" checkbox state, and the last used filename via `localStorage`.
* **User-Friendly Interface:** Clean layout with loading indicators and modal messages for feedback.

## How to Use

1.  **Open the `index.html` file** in your web browser.
2.  **Enter a VNDB ID or URL** into the input field. Examples:
    * `17`
    * `v17`
    * `https://vndb.org/v17`
    * `https://vndb.org/v17/chars`
3.  **Click the "Extract Character Info" button.**
    * If cached data exists, you'll be asked if you want to load it or fetch new data.
4.  **View the extracted information** in the "Extracted Information" section.
5.  **(Optional) Use Output Options:**
    * Enter text in the "Template" field.
    * Check "Include template in output" to prepend your template to the results.
    * Modify the suggested "Filename" if desired.
    * Click "Copy to Clipboard" or "Save to File".
6.  **(Optional) Save Settings:** Click the "Save Settings" button in the footer to persist your template, checkbox state, and filename for future sessions.

## Technical Details

* **Client-Side Application:** Runs entirely in the user's web browser using HTML, CSS (Tailwind CSS), and JavaScript.
* **CORS Proxy:** Uses `https://api.allorigins.win/raw?url=` to bypass Cross-Origin Resource Sharing (CORS) restrictions when fetching content from VNDB.
* **Local Storage:** Utilizes the browser's `localStorage` for:
    * Caching extracted character data to reduce redundant fetches.
    * Persisting user settings (template, filename, checkbox state).
* **HTML Parsing:** Parses the fetched HTML content to find relevant character data. This means the tool's functionality is dependent on the stability of VNDB's page structure.

## Disclaimer

* This tool relies on the specific HTML structure of VNDB character pages. If VNDB updates its website structure, this tool may break or require updates to its parsing logic.
* The functionality is also dependent on the availability and reliability of the CORS proxy (`api.allorigins.win`). If the proxy is down or blocks requests to VNDB, the tool will not be able to fetch data.
* Always respect VNDB's terms of service. This tool is intended for personal convenience.
