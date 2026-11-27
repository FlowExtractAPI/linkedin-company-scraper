**[LinkedIn Company Scraper](https://apify.com/dz_omar/linkedin-company-scraper?fpr=smcx63)** extracts **full LinkedIn company profiles in bulk** — paste a list of company URLs (or just their slugs) and get **one clean row per company**: industry, size, followers, headquarters, every office location, specialties, recent posts, employees and similar companies.

**No login. No cookies. No browser extension.** Perfect for **sales teams**, **recruiters**, **market researchers** and **data engineers** who need company data at scale.

## What does LinkedIn Company Scraper do?

- **Unlimited companies per run** — pass an array; duplicates are collapsed automatically.
- **Real numbers** — `employee_count: 217966`, not `"217,966"`.
- **Split addresses** — street, city, region, postal code and country code.
- **Clean specialties** — a proper list, not a mangled string.
- **Company posts** — with post ID, permalink and integer counts.
- **Nothing disappears silently** — a company that fails comes back as a row with the reason.

| | 🏢 This Actor | Typical alternatives |
|---|---|---|
| **Companies per run** | ✅ **Unlimited** — pass an array | ❌ One URL per run |
| **Numbers** | ✅ Real integers — `217966` | ❌ Strings — `"217,966"` |
| **Addresses** | ✅ Split into street / city / region / postal / country | ❌ One concatenated string |
| **Specialties** | ✅ Clean list | ❌ Last item mangled to `"and Telephone Support"` |
| **Company posts** | ✅ With post ID + permalink, counts as integers | ❌ Counts as strings, no post ID |
| **Failed companies** | ✅ Delivered as a row with the reason | ❌ Silently missing |
| **Duplicate inputs** | ✅ Collapsed automatically | ❌ Fetched twice |

### What data can you extract from LinkedIn company pages?

| Category | Fields |
|---|---|
| 🏢 Profile | name, LinkedIn company ID, slug, "About us" description, website (redirect unwrapped), industry, company type, founding year (number), specialties |
| 📈 Size & reach | employee count (number), size band (e.g. `10,001+ employees`), follower count (number) |
| 📍 Locations | HQ line, structured HQ address, **every** office location with the HQ flagged and a map link |
| 🖼️ Media | logo URL, cover / banner image URL |
| 👥 People & related pages | employees (name, profile URL, photo), similar companies, affiliated & showcase pages |
| 📣 Posts | post ID, permalink, full text, reaction count and types, comment count, images, video flag |
| 🧾 Run metadata | `input_url`, `scraped_at`, `success`, `error_type`, `error_message` |

### Why scrape LinkedIn company pages?

- **🎯 Lead generation & CRM enrichment** — turn company names into industry, size, HQ, website and headcount.
- **📊 Market & competitor research** — pull an industry cohort in one run, then follow `similar_pages` to find competitors you did not know to ask for.
- **🧑‍💼 Recruiting & talent mapping** — headcount, office locations and affiliated brands.
- **💰 Investment & vendor screening** — company type, founding year, footprint and specialties side by side.
- **📣 Social listening** — recent company posts with reaction and comment counts.
- **🔗 Data pipelines** — a stable `company_id` is a reliable join key across runs.

### Why use LinkedIn Company Scraper on Apify?

Running it on Apify gives you **API access**, **scheduling**, **monitoring**, **integrations** (Make, Zapier, n8n, webhooks) and **proxy rotation** without managing infrastructure. A 40-company run finished in about 20 seconds.

## How to scrape LinkedIn company pages

1. Open [LinkedIn Company Scraper](https://apify.com/dz_omar/linkedin-company-scraper?fpr=smcx63) in Apify Console.
2. Paste company URLs or plain slugs (`apple`, `microsoft`, `nvidia`) into **Company URLs**.
3. Optionally set **Concurrency** (default `5`, range `1`–`10`).
4. Turn off **employees**, **similar pages** or **affiliated pages** if you want a lean, flat row per company.
5. Click **Start**, then download the results as JSON, CSV or Excel, or fetch them over the API.

## How much does it cost to scrape LinkedIn company pages?

Runs are billed through your Apify plan. Start with a few companies to see the cost of a run in the Console before scaling up. Any change to the pricing is shown in the Apify Store before you run.

## Input and output examples

### Input

```json
{
    "companyUrls": [
        "https://www.linkedin.com/company/apple",
        "https://www.linkedin.com/company/microsoft",
        "https://de.linkedin.com/company/sap",
        "nvidia"
    ],
    "concurrency": 5,
    "includeEmployees": true,
    "includeSimilarPages": true,
    "includeAffiliatedPages": true
}
```

| Field | Type | Default | What it does |
|---|---|---|---|
| `companyUrls` | array | — (required) | Companies to scrape; mix URL formats and bare slugs freely |
| `concurrency` | integer | `5` | Companies fetched in parallel (`1`–`10`) |
| `includeEmployees` | boolean | `true` | Include the employee listing shown on the company page |
| `includeSimilarPages` | boolean | `true` | Include the "similar companies" LinkedIn recommends |
| `includeAffiliatedPages` | boolean | `true` | Include affiliated / showcase pages of the same organization |

### Supported LinkedIn URL types

| Input type | Example | Status |
|---|---|---|
| **Bare slug** | `apple` | ✅ Supported |
| **Company page** | `https://www.linkedin.com/company/apple` | ✅ Supported |
| **Showcase page** | `https://www.linkedin.com/showcase/appledeveloper/` | ✅ Supported |
| **School page** | `https://www.linkedin.com/school/mit/` | ✅ Supported |
| **Country subdomain** | `https://de.linkedin.com/company/sap` | ✅ Supported |
| **With tracking params** | `https://www.linkedin.com/company/apple?trk=abc` | ✅ Supported |
| **Sub-tab URL** | `https://www.linkedin.com/company/apple/about/` | ✅ Supported |
| **Personal profile** | `https://www.linkedin.com/in/someone` | ❌ Not a company page |

### Output

Each dataset item is one company:

```json
{
    "company_id": "162479",
    "universal_name_id": "apple",
    "company_name": "Apple",
    "description": "We're a diverse collective of thinkers and doers, continually reimagining what's possible…",
    "website": "http://www.apple.com/careers",
    "industry": "Computers and Electronics Manufacturing",
    "company_type": "Public Company",
    "founded_year": 1976,
    "specialties": [
        "Innovative Product Development",
        "World-Class Operations",
        "Retail",
        "Telephone Support"
    ],
    "employee_count": 217966,
    "employee_count_range": "10,001+ employees",
    "followers": 18407827,
    "headquarters": "Cupertino, California",
    "hq_address": {
        "street": "1 Apple Park Way",
        "city": "Cupertino",
        "region": "California",
        "postal_code": "95014",
        "country_code": "US"
    },
    "locations": [
        {
            "address": "1 Apple Park Way Cupertino, California 95014, US",
            "is_primary": true,
            "map_url": "https://www.bing.com/maps?where=1+Apple+Park+Way+Cupertino+95014+California+US"
        }
    ],
    "logo_url": "https://media.licdn.com/dms/image/v2/.../apple_logo",
    "cover_image_url": "https://media.licdn.com/dms/image/v2/.../apple_cover",
    "employees": [
        {
            "name": "Paul King",
            "profile_url": "https://www.linkedin.com/in/pdking",
            "image_url": "https://media.licdn.com/dms/image/v2/...",
            "is_anonymized": false
        }
    ],
    "updates": [],
    "similar_pages": [
        {
            "name": "Google",
            "url": "https://www.linkedin.com/company/google",
            "industry": "Software Development",
            "location": "Mountain View, CA",
            "logo_url": "https://media.licdn.com/dms/image/v2/.../google_logo"
        }
    ],
    "affiliated_pages": [
        {
            "name": "Apple Developer",
            "url": "https://www.linkedin.com/showcase/appledeveloper/",
            "industry": "Software Development",
            "location": null,
            "logo_url": "https://media.licdn.com/dms/image/v2/.../appledeveloper_logo"
        }
    ],
    "url": "https://www.linkedin.com/company/apple",
    "input_url": "apple",
    "scraped_at": "2026-09-07T19:05:24.436Z",
    "success": true,
    "error_type": null,
    "_source": "linkedin-company-scraper",
    "source_url": "https://www.linkedin.com/company/apple"
}
```

### Company post record

Companies that post publicly return their recent updates in `updates`:

```json
{
    "post_id": "7502733677454512128",
    "activity_urn": "urn:li:activity:7502733677454512128",
    "url": "https://www.linkedin.com/feed/update/urn:li:activity:7502733677454512128/",
    "content": "Tired of choice overload?\n\nSmart Routing takes the guesswork out by automatically matching your tasks to the right model.",
    "posted_ago": "4h",
    "reactions": 188,
    "reaction_types": ["LIKE", "INTEREST", "EMPATHY"],
    "comments": 13,
    "images": ["https://media.licdn.com/dms/image/v2/..."],
    "has_video": false
}
```

### Failed company record

A company that cannot be scraped is still delivered:

```json
{
    "universal_name_id": "example-that-404s",
    "url": "https://www.linkedin.com/company/example-that-404s",
    "input_url": "example-that-404s",
    "success": false,
    "error_type": "NOT_FOUND",
    "error_message": "Company page not found: example-that-404s",
    "scraped_at": "2026-09-07T19:05:24.436Z"
}
```

### Dataset views

| View | What it shows |
|---|---|
| 🏢 **Company Overview** | Name, industry, type, size, followers, HQ, website |
| 📝 **Full Profile** | Description, specialties, split address, all locations, imagery |
| 📣 **Company Posts** | Recent posts with reactions and comments |
| 🌐 **People & Related Pages** | Employees, similar companies, affiliated pages |
| ⚠️ **Failed Companies** | Anything that could not be scraped, and why |

## Other Actors you might need

<!-- RECOMMENDED:START (generated by apify-actor-forge/tools/recommend.py; edits inside are overwritten) -->

| Actor | What it adds |
|---|---|
| **[LinkedIn Ads Scraper](https://apify.com/dz_omar/linkedin-ads-scraper?fpr=smcx63)** | Extract comprehensive LinkedIn ads data from the Ad Library. |
| **[LinkedIn Jobs Scraper](https://apify.com/dz_omar/linkedin-jobs-scraper?fpr=smcx63)** | LinkedIn job postings with salary ranges, applicant counts & the recruiter who posted |
| **[Skool Members Scraper](https://apify.com/dz_omar/skool-map-scraper?fpr=smcx63)** | Map Location, Country Filter & Socials |
| **[Facebook Ads Scraper Pro](https://apify.com/dz_omar/facebook-ads-scraper-pro?fpr=smcx63)** | Extract Facebook Ad Library data: creatives, targeting & metrics. |
| **[Facebook Comment Scraper](https://apify.com/dz_omar/facebook-comment-scraper?fpr=smcx63)** | Comments & threaded replies from Facebook reels, videos, photos, posts & groups |

<!-- RECOMMENDED:END -->

## Frequently asked questions

### Do I need a LinkedIn account or cookies?

No. The Actor only reads public company pages — no login, no cookies, and your LinkedIn account is never involved.

### How many companies can I scrape in one run?

As many as you like — pass them all in `companyUrls`. Very large lists are capped at 10,000 companies per run; split bigger jobs across runs.

### Why did a well-known company come back as `NOT_FOUND`?

Its slug is probably different from what you guessed: `intel` is a 404 — the real page is `intel-corporation`; the same is true of `mongodb`, `redis`, `plaid` and others. Copy the URL from LinkedIn, and check the ⚠️ Failed Companies view.

### Why are some employees unnamed?

LinkedIn withholds some identities on public company pages. Those rows carry `is_anonymized: true` with a `null` name and profile URL, so you can tell "LinkedIn hid this" apart from "the scraper missed it". The Actor already retries to land on the variant that names them.

### Why is `founded_year`, `specialties` or `cover_image_url` empty for some companies?

The company did not publish it. Roughly a third of company pages omit a founding year, and most have no cover image — empty means absent at the source, not a scraping failure.

### Can I get employee job titles?

Not from the public company page — LinkedIn no longer renders them there. You get name, profile URL and photo.

### Can I scrape showcase and school pages?

Yes. `linkedin.com/showcase/...` and `linkedin.com/school/...` both work and return the same record shape.

### Will duplicates in my list be fetched twice?

No. `apple`, `https://www.linkedin.com/company/apple` and `https://fr.linkedin.com/company/APPLE?trk=x` are recognised as the same company and fetched once.

### What if I paste a personal profile by mistake?

It is skipped with a clear warning, and the rest of the run continues normally.

### Can I use LinkedIn Company Scraper in Make, Zapier, n8n or my own code?

Yes — through Apify's integrations, or with the Apify API and client libraries.

## Support

- 🌐 **Website:** [flowextractapi.com](https://flowextractapi.com)
- 📧 **Email:** [support@flowextractapi.com](mailto:support@flowextractapi.com)
- 💬 **GitHub:** [FlowExtractAPI](https://github.com/FlowExtractAPI)
- 💼 **LinkedIn:** [flowextract-api](https://www.linkedin.com/in/flowextract-api/)
- 🐦 **X (Twitter):** [@FlowExtractAPI](https://x.com/FlowExtractAPI)
- 📱 **Facebook:** [flowextractapi](https://www.facebook.com/flowextractapi)
- 🎵 **TikTok:** [@flowextractapi](https://www.tiktok.com/@flowextractapi)

## Legal & compliance

- **Public data only** — public LinkedIn company pages, no login, no cookies, no account access.
- **Rate limiting** — modest request rates with back-off.
- **Data protection** — no storage of personal information or unauthorized data collection.
- **Commercial use** — suitable for business intelligence and research.
- No affiliation with or endorsement by LinkedIn is implied.

---

*LinkedIn Company Scraper — by FlowExtract API. Turn any website into structured data.*
