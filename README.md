# Advanced Manufacturing App Analytics Dashboard

This project is a Streamlit dashboard for monitoring downloads and usage of the Advanced Manufacturing App. It combines data from Apple App Store Connect, Google Play, and Google Analytics 4 so a non-technical owner can quickly see whether people are finding, downloading, opening, and using the app.

## What This Dashboard Shows

The dashboard includes:

- **Store downloads** from Apple App Store Connect and Google Play.
- **Active users, total users, new users, and returning users** from Google Analytics 4.
- **Screen views and session starts** from Google Analytics 4.
- **Average engagement time** so you can see whether users are spending meaningful time in the app.
- **Realtime activity** for users active in the last 30 minutes.
- **Device models and device categories** to understand what devices people use.
- **Downloads by Apple vs Android** to compare platform performance.
- **Daily, weekly, and monthly line-chart views** for trends.
- **Comparison periods** so you can compare one date range against another.
- **Growth diagnostics** for acquisition channels, source/medium, campaigns, geography, app version, operating system, and top app events.

## Why It Exists

The dashboard is meant to answer practical marketing and product questions:

- Are app downloads increasing?
- Are display ads or organic social campaigns leading to more app starts?
- Are users coming back after first use?
- Which devices, countries, or traffic sources are strongest?
- Is the app getting downloads but not first opens?
- Are people actually engaging once they open the app?

## How To Use It

1. Open the deployed Streamlit app.
2. Choose a **Start date** and **End date** in the sidebar.
3. Choose the line chart breakdown: **Daily**, **Weekly**, or **Monthly**.
4. Optional: turn on **Compare with another period** to compare KPIs against a prior date range.
5. Click **Refresh data** if you want the dashboard to clear cached results and pull fresh data.

## Important Notes About Timing

Store reporting is not always instant.

- **Google Analytics 4** usage data is usually available sooner.
- **Apple App Store Connect** sales/download reports may lag.
- **Google Play** bulk reports may lag and can update later than GA4.

Because of this, a recent date may show GA4 activity before store downloads are fully available.

## Current Campaign Note

Display ads on **advancedmanufacturing.org** started on **August 6, 2026** for targeted devices to drive app downloads. They are planned to run through **December 2026**. Organic social promotion is also active. Paid social has not started yet unless noted separately.

## What The Main KPIs Mean

- **Store downloads**: downloads reported by Apple App Store Connect and Google Play.
- **Active users**: users who actively used the app during the selected date range.
- **Total users**: total GA4 users during the selected date range.
- **New users**: users who were new during the selected date range.
- **Returning users**: pulled directly from GA4 using the `newVsReturning = returning` user group.
- **Screen views**: app screens viewed during the selected date range.
- **Session starts**: number of GA4 `session_start` events.
- **Avg engagement / active user**: total engagement time divided by active users.

## Data Sources

### Google Analytics 4

Used for app usage, engagement, realtime users, devices, geography, traffic source, campaigns, events, screen views, session starts, and returning users.

The GA4 property ID and service account credentials are stored in Streamlit secrets for deployment.

### Google Play

Used for Android download reporting through Google Play bulk install reports.

### Apple App Store Connect

Used for iOS download reporting through App Store Connect Sales and Trends reports.

## Credentials And Ownership

The deployed dashboard reads credentials from **Streamlit Cloud secrets**. The secrets should not be committed to GitHub.

Based on the current setup, the important credentials are service-account or team-level credentials and are expected to keep working as long as the underlying accounts, permissions, and API keys remain active.

A future owner should have access to:

- The Streamlit Cloud app and its secrets.
- The GitHub repository.
- The GA4 property.
- The Google Cloud project that owns the service account.
- Google Play Console reporting access.
- App Store Connect API key access.

## Files In This Project

| File or folder | Purpose |
| --- | --- |
| `app.py` | Main Streamlit dashboard. |
| `store_downloads.py` | Pulls and parses Apple App Store Connect and Google Play download data. |
| `requirements.txt` | Python packages needed to run the dashboard. |
| `README.md` | This handoff guide. |
| `config/app_store_sources.example.json` | Example local store-download configuration with fake placeholder values. |
| `.streamlit/secrets.toml.example` | Example Streamlit secrets structure. |
| `.streamlit/secrets.toml.template` | More complete local secrets template. |
| `.gitignore` | Prevents secrets, local config, virtual environments, and cache files from being committed. |

Local files such as real service account JSON files, real App Store keys, and `.streamlit/secrets.toml` are intentionally ignored by Git.

## Running Locally

Most non-technical users will use the deployed Streamlit app and will not need this section.

For local testing:

```powershell
pip install -r requirements.txt
streamlit run app.py
```

Local credentials can be supplied either through `.streamlit/secrets.toml` or environment variables. Do not commit real credential files.

For local store-download configuration, the app checks these places:

1. `APP_STORES_CONFIG`, if that environment variable is set.
2. A neighboring Scorecards config at `../Scorecards/config/google_play_sources.json`, if it exists.
3. `config/app_store_sources.json`, if present locally.

For Streamlit Cloud, the deployed app should use Streamlit secrets instead of local files.

## Deployment

The dashboard is designed to run on Streamlit Cloud from the GitHub repository.

When code is pushed to GitHub, Streamlit Cloud should redeploy automatically. If it does not, open the Streamlit Cloud app settings and manually reboot or redeploy the app.

## Common Troubleshooting

### The dashboard says data could not be loaded

Check Streamlit Cloud logs. The most common causes are missing secrets, expired/revoked credentials, or a service account losing access to GA4, Google Play, or App Store Connect.

### Downloads are lower than expected or show zero for recent dates

Recent store data may not be available yet. Google Play and App Store Connect can lag behind GA4. Check the dashboard notes under **Download source notes**.

### GA4 users appear but store downloads do not

This can happen when store reports have not caught up yet, or when users open the app from installs that happened before the selected date range.

### Returning users do not equal active users minus new users

That is expected. Returning users are pulled directly from GA4's `newVsReturning` grouping, which may not equal a simple subtraction.

### A chart looks empty

Try a wider date range or click **Refresh data**. Some metrics may not exist for very short or very recent date ranges.

## Handoff Checklist

Before transferring ownership, confirm that the new owner can access:

- Streamlit Cloud app settings and secrets.
- GitHub repository settings.
- GA4 property access.
- Google Cloud service account access.
- Google Play Console reports.
- App Store Connect API keys and Sales and Trends reports.

Also confirm that the dashboard still loads after the new owner signs in to Streamlit Cloud.

## Maintenance Notes

- Do not place real secrets in GitHub.
- Keep `.gitignore` protections in place.
- Use the **Refresh data** button before assuming recent data is final.
- If adding new GA4 fields, test them locally first because GA4 rejects unsupported dimensions or metrics.
- If the app breaks after a dependency update, check `requirements.txt` and Streamlit Cloud logs first.
