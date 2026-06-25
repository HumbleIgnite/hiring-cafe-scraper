[Hiring Cafe Scraper](https://apify.com/manojachari/hiring-cafe-scraper?fpr=data)

Scrape thousands of job listings from [hiring.cafe](https://hiring.cafe) in seconds. Get structured data with direct apply links, company names, locations, seniority levels, and engagement metrics — ready for spreadsheets, dashboards, or your own job search tool.

## What is hiring.cafe?

[Hiring.cafe](https://hiring.cafe) is a job aggregation platform that indexes millions of job listings from thousands of companies. It pulls from major job boards like Greenhouse, Lever, Workable, Workday, BambooHR, and company career pages — giving you a single source to search across all of them.

## What does this Actor do?

This Actor searches hiring.cafe using its internal API and returns clean, structured job data. It handles Cloudflare protection automatically using an anti-detect browser, so you get reliable results every time.

**How it works:**

1. Launches a stealth browser to establish a session with hiring.cafe
2. Bypasses Cloudflare Turnstile challenge automatically
3. Queries the hiring.cafe search API with your filters
4. Returns structured JSON data for each job listing

## Features

- **Keyword search** — Search for any job title, skill, or keyword
- **Location filtering** — Filter by country: United States, United Kingdom, Canada, Germany, India
- **Workplace type** — Remote, Hybrid, or Onsite
- **Seniority level** — No Prior Experience, Entry Level, Mid Level, Senior Level
- **Commitment type** — Full Time, Part Time, Contract, Internship, Temporary, Seasonal, Volunteer
- **Industry filtering** — 34 industries including AI & Machine Learning, Fintech, SaaS, Healthcare, Cybersecurity, and more
- **Company filtering** — Include or exclude specific companies by name
- **Date filtering** — Only get jobs posted within the last N days (1–365)
- **Engagement metrics** — See how many people viewed, applied to, and saved each listing
- **Budget control** — Automatically stops when your max charge limit is reached

## Output

Each job listing includes:

| Field | Type | Description |
| --- | --- | --- |
| `id` | string | Unique job listing ID |
| `title` | string | Job title |
| `source` | string | Company name |
| `apply_url` | string | Direct link to apply |
| `board_token` | string | Job board identifier |
| `description` | string | Full job description (HTML cleaned) |
| `location` | string | City, state/region, country |
| `workplace_type` | string | Remote, Hybrid, or Onsite |
| `seniority` | string | Experience level required |
| `commitment_type` | string | Full Time, Part Time, Contract, etc. |
| `posted_at` | string | ISO 8601 timestamp of when the job was posted |
| `industry` | string | Industry or job category |
| `viewed_count` | number | Number of views on hiring.cafe |
| `applied_count` | number | Number of applications via hiring.cafe |
| `saved_count` | number | Number of saves on hiring.cafe |

## Example use cases

- **Job seekers** — Build a personal job tracker with fresh listings updated daily
- **Recruiters** — Monitor competitor hiring patterns across industries
- **Market researchers** — Analyze hiring trends by role, location, or industry
- **HR teams** — Benchmark job titles, seniority levels, and commitment types in your market
- **Data analysts** — Feed structured job data into dashboards or ML pipelines

## Input examples

### Find remote product manager jobs posted this week

```
{
    "searchQuery": "product manager",
    "workplaceTypes": ["Remote"],
    "seniorityLevels": ["Mid Level", "Senior Level"],
    "commitmentTypes": ["Full Time"],
    "dateFetchedPastNDays": 7,
    "maxResults": 100
}
```

### Find entry-level AI jobs in the US

```
{
    "searchQuery": "machine learning engineer",
    "location": "United States",
    "workplaceTypes": ["Remote", "Hybrid"],
    "seniorityLevels": ["Entry Level", "No Prior Experience Required"],
    "industries": ["AI & Machine Learning"],
    "dateFetchedPastNDays": 30
}
```

### Monitor a specific company's hiring

```
{
    "searchQuery": "",
    "companyNames": ["Google", "Meta", "Apple"],
    "location": "United States",
    "dateFetchedPastNDays": 7
}
```

## Proxy configuration

This Actor requires a real browser to bypass Cloudflare protection. **Residential proxies are required** for reliable results on Apify cloud.

In the proxy settings, enable:

- **Use Apify Proxy**: Yes
- **Proxy groups**: `RESIDENTIAL`

Without residential proxies, Cloudflare will block the requests.

## Pricing

This Actor uses pay-per-result pricing:

| Component | Cost |
| --- | --- |
| Start fee | $0.01 per run |
| Per result | $0.003 per job listing |

**Examples:**

- 100 jobs = **$0.31**
- 500 jobs = **$1.51**
- 1,000 jobs = **$3.01**
- 5,000 jobs = **$15.01**

Set a **max charge limit** on your run and the Actor will automatically stop before exceeding it.

## Limitations

- **Location presets** — Currently supports 5 country-level locations (US, UK, Canada, Germany, India). City-level filtering is not yet supported.
- **Cloudflare dependency** — The Actor needs to pass Cloudflare's challenge on each run, which adds ~10–20 seconds of startup time.
- **Data freshness** — Results come directly from hiring.cafe's index. Some listings may be stale if the original job board hasn't been re-crawled recently.
- **Residential proxies required** — Datacenter proxies will be blocked by Cloudflare. Residential proxy usage incurs additional Apify platform costs.

## Changelog

- **1.0** — Initial release with keyword search, location/workplace/seniority/commitment/industry filters, engagement metrics, and Cloudflare bypass via Camoufox.