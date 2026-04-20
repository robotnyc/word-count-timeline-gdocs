# Word Count Timeline Google Docs Editor Add-on

An add-on to track your writing productivity in Google Docs by visualizing your word and edit count changes over time.

This add-on only tries to use only read-only access so your documents stay safe and secure. It is developed in Apps Script.

## Features

1. Track word count by document and by chapter against an optional goal count (stored in an Apps Script property).
2. Session word count changes over time (group revisions by 60 minute sessions). This uses the Google Drive revisions API.
3. Track edits vs new words added by diff'ing document revisions.
4. Only the first Document Tab is counted. Move notes, edits, drafts, etc... into another tab so they are not counted.

### Visualizations

1. The word count goal tracker either weekly or daily.
2. The Heatmap: A visual grid (X: Hour of Day, Y: Day of Week) showing when the most words are typically added.
3. The 'Golden Hour': A card displaying the user's statistically most productive 60-minute window.
4. Velocity Meter: Show 'Words per Minute' for the current session vs. all-time average.
5. Chapter Breakdown: Parse 'Heading 1' styles from the doc to show word counts and progress bars per chapter.

## Usage

1. From the Google Docs "Extensions" menu, search for "Word Count Timeline".
2. Authenticate with Google OAuth 2.0 and allow scopes documents.readonly and drive.metadata.readonly.
3. Activate the add-on from the side bar to see your writing stats.
4. Add-on runs automatically at least once an hour in order to refresh statistics.

## Development

The repository is structured as an [Apps Script](https://developers.google.com/apps-script) project. You can manage it with [clasp](https://github.com/google/clasp) or directly from the Apps Script editor:

1. Install [clasp](https://github.com/google/clasp#installation) and authenticate (`clasp login`).
2. Run `clasp create --type docs --title "Word Count Timeline"` or clone an existing script if configured.
3. Push the local files with `clasp push`, then open the script in the online editor (`clasp open`).
4. Use `onOpen` to add the menu and `showSidebar` to preview the sidebar UI.
5. Real API implementations live in `Data.gs`.
6. Use `clasp push --watch --force` when making changes to automatically push local changes (including those to the manifest).

## Limitations

1. The add-on is not able to fetch the word count for the very first revision of a document.
2. The add-on is only able to fetch the word count by section for the current document. Past revisions are only able to fetch the total word count.
3. Revision history is not reliable. For example, after 3 months Google Drive can merge previous revisions. Unless they are named.

## TODO

1. Add fail handler and error page for all methods. https://developers.google.com/apps-script/guides/html/reference/run#withFailureHandler(Function)
2. Adjust UTC time for local timezone so changes appear on the correct date.
3. Add word count goal and display progress towards goal. Divide goal by the number of chapters/headings to determine per-chapter progress.
