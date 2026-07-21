# LEF to TAR Converter

A lightweight, client-side web application designed to process, extract, and repackage `.lef` files. 

Often, these files contain valid ZIP archives obscured by prepended junk data. This tool hunts for the raw ZIP signature (`PK\x03\x04`), strips the junk, extracts the contents, and repackages them into standard uncompressed POSIX `.tar` files. 

## Features

* **100% Local Processing:** All file parsing, extraction, and repackaging happens directly in your browser's memory. **Zero data is transmitted to any server**, ensuring complete privacy and security for sensitive files.
* **Junk Header Stripping:** Automatically handles `.lef` files that standard extraction tools reject by scanning the raw binary for valid archive signatures.
* **Batch Processing:** Drag and drop multiple files at once. The tool will process them sequentially and bundle the resulting `.tar` files into a single `.zip` for easy downloading.
* **Zero Dependencies:** Runs on a single static `index.html` file utilizing [JSZip](https://stuk.github.io/jszip/) via CDN.

## How to Use

1. Navigate to the GitHub Pages deployment URL (or simply open `index.html` in your web browser).
2. Drag and drop your `.lef` files into the designated drop zone, or click to select files from your computer.
3. Wait for the processing log to indicate success.
4. Click the **Download Converted Package** button to save your bundled `.tar` files.

## Deployment

Since this tool requires no backend infrastructure, deployment is as simple as hosting a static site:

1. Upload `index.html` to a GitHub repository.
2. Navigate to **Settings** > **Pages**.
3. Under **Build and deployment**, select **Deploy from a branch**.
4. Choose the `main` branch (or whichever branch holds your `index.html`) and click **Save**.
5. Your applet will be live at `https://[your-username].github.io/[repository-name]/`.

## Technical Details

This applet replicates a Python environment's `zipfile` and `tarfile` behavior purely in JavaScript. It relies on the File API to read files as `ArrayBuffer`s, uses `JSZip` to mount the internal archives, and utilizes a custom-built lightweight `TarBuilder` class to format the output as standard `ustar` POSIX TAR blobs.
