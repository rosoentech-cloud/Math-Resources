# Rosoen student resources: upload and update guide

Everything the page needs is in `index.html`. You do not need any other file for the lesson list to load. The lesson cards and recording status are set in one block near the bottom of `index.html`, marked **RESOURCE CONFIGURATION**.

## 1. Upload to GitHub

1. Unzip the download. You will see `index.html`, `ADDING-RESOURCES.md`, `.nojekyll`, and a `downloads` folder.
2. In your repository, select **Add file > Upload files**. Drag in everything from the unzipped folder so these items sit at the top level of the repository, next to each other.
3. Select **Commit changes**.
4. In **Settings > Pages**, set **Source** to *Deploy from a branch*, choose your main branch, and keep the folder as `/ (root)`. Save, wait about a minute, then open your Pages address.

Keep `.nojekyll` in place. It tells GitHub Pages to serve every file as uploaded.

## 2. Add or replace a PPTX file

1. Open the `downloads` folder in GitHub and select **Add file > Upload files**. Use a file name with no spaces, for example `GED_Math_Fractions_without_notes.pptx`.
2. Open `index.html`, find the **RESOURCE CONFIGURATION** block, and add an entry to the `versions` list of the lesson it belongs to. Or add a new lesson at the end of `lessons`:

```
{
  "label": "Zoom edition",
  "file": "downloads/GED_Math_Fractions_without_notes.pptx",
  "slides": 12,
  "speakerNotes": "without",
  "available": true
}
```

3. Select **Commit changes**.

To replace a file, upload the new version with the same file name, then commit. Update `slides` if the slide count changed.

## 3. Add or update a recording

In the `recordings` list inside the same block, leave the entry as it is until the recording is ready:

```
{
  "title": "Zoom session recording",
  "status": "pending",
  "url": "",
  "pendingLabel": "Recording coming Thursday"
}
```

When the recording is ready, change it to:

```
{
  "title": "Zoom session recording",
  "status": "available",
  "url": "https://example.com/your-recording-link",
  "pendingLabel": "Recording coming Thursday"
}
```

The page then shows a **Watch recording** button and hides the "coming Thursday" message. Links must start with `https://`.

For the next session, add a second entry with `"status": "pending"` and an empty `url`.

## 4. Hide a file without deleting it

Set `"available": false` on that version. Set it back to `true` to show it again.

## 5. Speaker notes labels

Use one of these values for `speakerNotes`:

- `"without"` shows *Without speaker notes*
- `"with"` shows *With speaker notes*
- `"selected"` shows *Speaker notes on selected slides*

## Things to know

- Missing files are handled for you. When the page is served from GitHub Pages, it checks each file on load. If a file is not there, its button is hidden, so no broken download links appear.
- File sizes are read from the file when the server reports them. The `size` value is only a fallback, so you can leave it out.
- Every file in this repository is public, including anything in `downloads`. There is no login on this site. Do not upload passwords, private student information, or instructor-only material.
- Speaker notes in these files may contain answer keys and teaching scripts. The files here have had their notes removed. Only add a version with `"speakerNotes": "with"` after you have checked that students should see the notes.
- Keep the quotation marks, commas, and brackets exactly as they appear in the configuration block. A single missing comma stops the lesson list from showing, and the page then displays a message that points to the block. Use the **Preview changes** tab in GitHub before you commit.
