[Hiring Cafe Scraper](https://apify.com/abotapi/hiring-cafe-scraper?fpr=data)

# Hiring.Cafe Jobs Scraper

Extract structured job listings from Hiring.Cafe at scale. 100+ fields per job including salary, company funding data, benefits, certifications, and geo coordinates.

## Why This Scraper?

**Fast.** Each API call returns ~150 jobs. Scrape 500 jobs in under 30 seconds, 1,000 jobs in under a minute (after initial Cloudflare solve). Results are pushed incrementally so you can start processing before the run finishes.

**More Filters.** Employment type, seniority level, salary transparency, and date range filters that no other Hiring.Cafe scraper on Apify offers.

**Direct Job URLs.** Paste `/viewjob/` links alongside search URLs to scrape individual listings with full data.

**Total Count.** Shows how many jobs match your search before scraping begins.

## How It Works

### Option 1: Search by URL

Paste one or more search URLs from hiring.cafe. Go to [hiring.cafe](https://hiring.cafe), apply your filters, then copy the URL from the address bar.

You can also paste direct job URLs (`/viewjob/...`) to scrape individual listings.

### Option 2: Search by Filters

Use keyword, location, and advanced filters without building URLs.

```
{
  "keyword": "python developer",
  "location": "United States",
  "workplaceType": "Remote",
  "commitmentType": "Full Time",
  "seniorityLevel": "Senior Level",
  "salaryTransparentOnly": true,
  "maxItems": 500
}
```

## Filter Options

| Filter | Options | Default | Competitors |
| --- | --- | --- | --- |
| Keyword | Any text | (empty) | All have |
| Location | Country or city | (worldwide) | All have |
| Workplace Type | Remote, Hybrid, Onsite, Any | Any | All have |
| **Employment Type** | Full Time, Part Time, Contract, Internship, Any | Any | **Only us** |
| **Seniority Level** | Entry, Mid, Senior, No Experience, Any | Any | **Only us** |
| **Posted Within** | 1 to 365 days | 30 | **Only us** |
| **Salary Transparent** | true or false | false | **Only us** |

> **Note:** Hiring.Cafe uses relevance based search. Keyword and employment type are hard filters. Workplace type and seniority level influence ranking but are soft filters. For precise filtering, use URL mode with a hiring.cafe URL where you applied filters directly on the website.

## Output Structure (100+ fields)

Output preserves the native Hiring.Cafe nested format, fully compatible with other Hiring.Cafe scrapers on Apify.

### Top Level Fields

`id`, `board_token`, `source`, `apply_url`, `job_url`, `requisition_id`, `is_expired`

### Job Info

`title`, `job_title_raw`, `description` (full HTML)

### Job Details (91 fields)

| Category | Sample Fields |
| --- | --- |
| Title and Summary | core_job_title, requirements_summary, job_category |
| Skills | technical_tools[], licenses_or_certifications[] |
| Education | bachelors, masters, doctorate degree requirement, fields_of_study[] |
| Experience | min_industry_and_role_yoe, min_management_and_leadership_yoe |
| Employment | commitment[], role_type, seniority_level, workplace_type |
| Location | formatted_workplace_location, workplace_cities, states, countries[] |
| Compensation | yearly, monthly, weekly, hourly min and max compensation, currency |
| Benefits | visa_sponsorship, 401k_matching, four_day_work_week, retirement_plan |
| Work Conditions | physical_labor_intensity, travel_requirement, shift_work |
| Languages | language_requirements[], num_language_requirements |

### v5_processed_company_data (19 fields)

`name`, `homepage_uri`, `industries[]`, `nb_employees`, `year_founded`, `hq_country`, `organization_type`, `latest_funding_type`, `latest_funding_amount`, `investors[]`, `stock_exchange`, `stock_symbol`

### Geoloc

`lat`, `lon`

## Example Output

```
{
  "id": "lever___example___12345",
  "source": "lever",
  "board_token": "example",
  "apply_url": "https://jobs.lever.co/example/12345",
  "job_url": "https://hiring.cafe/viewjob/abc123xyz",
  "is_expired": false,
  "job_information": {
    "title": "Backend Engineer",
    "description": "<p>Job description HTML content...</p>"
  },
  "v5_processed_job_data": {
    "core_job_title": "Backend Engineer",
    "commitment": ["Full Time"],
    "seniority_level": "Mid Level",
    "workplace_type": "Remote",
    "formatted_workplace_location": "New York, New York, United States",
    "yearly_min_compensation": 120000,
    "yearly_max_compensation": 160000,
    "listed_compensation_currency": "USD",
    "is_compensation_transparent": true,
    "technical_tools": ["Node.js", "PostgreSQL", "AWS"],
    "visa_sponsorship": false,
    "company_name": "Example Inc"
  },
  "v5_processed_company_data": {
    "name": "Example Inc",
    "nb_employees": 200,
    "year_founded": 2018,
    "hq_country": "US",
    "organization_type": "Private",
    "latest_funding_type": "Series A",
    "latest_funding_amount": 15000000
  },
  "_geoloc": [{"lat": 40.7128, "lon": -74.006}]
}
```

## Input Options

| Field | Description | Default |
| --- | --- | --- |
| Start URLs | Search URLs or job URLs from hiring.cafe |  |
| Keyword | Job title, skills, or company name |  |
| Location | Country or city | (worldwide) |
| Workplace Type | Remote, Hybrid, Onsite, Any | Any |
| Employment Type | Full Time, Part Time, Contract, Internship, Any | Any |
| Seniority Level | Entry, Mid, Senior, Any | Any |
| Posted Within | Days since posted (1 to 365) | 30 |
| Salary Transparent | Only jobs with disclosed salary | false |
| Max Jobs | Maximum listings to scrape | 1000 |

## Tips

The total count shows before scraping so you know the search size upfront.

You can combine `/viewjob/` URLs with search URLs in a single run.

For precise location filtering, apply your filters on hiring.cafe first, then paste the URL into Start URLs.