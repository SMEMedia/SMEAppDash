# Advanced Manufacturing App Analytics Dashboard

This dashboard combines Apple App Store Connect, Google Play, and Google Analytics 4 information to show how people find, download, open, and use the Advanced Manufacturing app.

## Important links

- [Open the App Analytics Dashboard](https://smeappdash.streamlit.app/)
- [SMEMedia repository](https://github.com/SMEMedia/SMEAppDash)

## Use the dashboard

1. Choose the start and end dates.
2. Choose a **Daily**, **Weekly**, or **Monthly** chart view.
3. Optionally select **Compare with another period**.
4. Select **Refresh data** when a new pull is needed.
5. Review downloads, users, engagement, screen views, session starts, devices, sources, campaigns, geography, app versions, and events.

## Understand reporting delays

Google Analytics usage information often appears before Apple and Google Play store reports. Recent dates can therefore show app activity before store downloads are complete. Store totals may increase after the reporting platforms finish processing.

Returning users come directly from Google Analytics and may not equal active users minus new users.

## Troubleshooting

### Recent downloads are zero or lower than expected

- Check the dashboard’s **Download source notes**.
- Widen the date range to include several earlier days.
- Wait for Apple and Google Play reporting to finalize.
- Compare Apple and Android separately to identify which source is delayed.

### Google Analytics users appear but store downloads do not

- This can be a normal timing difference.
- The selected users may also have installed the app before the selected period.
- Check again after the store reporting delay.

### A chart is empty

- Try a wider date range.
- Select **Refresh data** once.
- Confirm the selected comparison period is valid.
- Check whether the metric is available for the selected platform and dates.

### The dashboard says information could not be loaded

- Note which source is named in the message.
- Refresh once; do not repeatedly request new data.
- If the same source fails, send the source name, date range, time, and screenshot to support.
- The Streamlit owner should review the app status and saved source connections.

### Results changed after a report was shared

- Recent platform data can be revised.
- Confirm the original and current reports use identical date ranges and filters.
- Record when each report was refreshed.
- Use finalized periods for recurring executive reporting whenever possible.

### The dashboard does not open after an update

- Refresh the browser or try a private window.
- Check [Streamlit Community Cloud](https://share.streamlit.io/) for an app status message.
- If the app shows a deployment or credential error, contact the assigned technical owner.

## Ongoing maintenance

- Use **Refresh data** before concluding that recent information is final.
- Keep GA4, Google Cloud, Google Play, App Store Connect, Streamlit, and repository access assigned to current SME staff.
- Review source-account permissions when staffing or ownership changes.
- Escalate credential, reporting-source, deployment, and code changes to the assigned technical owner.
