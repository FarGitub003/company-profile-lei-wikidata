# Company Profile from Wikidata + GLEIF (LEI)

One structured profile per company name, LEI or Wikidata ID: legal identity, LEI status and renewal, parents, website, industry, size, revenue, listings, social links. Official open data (GLEIF + Wikidata, CC0), no key. Pay per profile found; not found and ambiguous are free.

**▶ Run it on Apify Store: https://apify.com/far003/company-profile-lei-wikidata**

> This repository hosts documentation and examples; the Actor runs on the Apify platform.

## What it does

- Returns one structured profile per company name, LEI or Wikidata ID: legal identity, LEI status and renewal, parent companies, website, industry, size, revenue, stock listings and social links.
- Joins GLEIF (legal entity data) and Wikidata (business data) only through the LEI written on the Wikidata item.
- A name that fits several companies comes back as `ambiguous` with the candidates, never as a guess.
- Every record says how it was matched (`matchConfidence` + `matchExplanation`) and carries the exact source URLs.
- No API key and no scraping of company websites.

## Who it is for

- KYC and compliance checks.
- Sales intelligence and CRM enrichment.
- Research that needs a legal identity tied to a company name.

## Example input

The example output below is a real run on this LEI. You can also pass company names or Wikidata IDs (for example `Apple Inc.` or `Q312`).

```json
{
    "companies": [
        "HWUPKR0MPOU8FGXBT394"
    ]
}
```

## Example output

A found profile (real run, input `HWUPKR0MPOU8FGXBT394`):

<details><summary>Show the record</summary>

```json
{
  "query": "HWUPKR0MPOU8FGXBT394",
  "matchType": "lei",
  "status": "found",
  "statusMessage": "Profile found.",
  "matchConfidence": "high",
  "matchExplanation": "The LEI was given and exists in GLEIF. Wikidata item Q312 carries the same LEI (P1278).",
  "name": "Apple Inc.",
  "lei": "HWUPKR0MPOU8FGXBT394",
  "legalName": "Apple Inc.",
  "otherNames": [
    {
      "name": "Apple Computer, Inc.",
      "type": "PREVIOUS_LEGAL_NAME",
      "language": "en"
    }
  ],
  "entityStatus": "ACTIVE",
  "entityCategory": "GENERAL",
  "registrationStatus": "ISSUED",
  "leiLapsed": false,
  "renewalOverdue": false,
  "nextRenewalDate": "2027-03-08T17:27:20Z",
  "initialRegistrationDate": "2012-06-06T15:53:00Z",
  "lastUpdateDate": "2026-03-03T16:34:33Z",
  "legalForm": {
    "code": "H1UM",
    "name": "For-Profit Corporation General Stock"
  },
  "jurisdiction": "US-CA",
  "registrationAuthority": {
    "id": "RA000598",
    "name": "Business Entity Records",
    "website": "https://businesssearch.sos.ca.gov/",
    "entityId": "806592"
  },
  "legalAddress": {
    "lines": [
      "C/O C T Corporation System",
      "330 N. Brand Blvd",
      "Suite 700"
    ],
    "city": "Glendale",
    "region": "US-CA",
    "country": "US",
    "postalCode": "91203",
    "formatted": "C/O C T Corporation System, 330 N. Brand Blvd, Suite 700, 91203 Glendale, US-CA, US"
  },
  "headquartersAddress": {
    "lines": [
      "One Apple Park Way"
    ],
    "city": "Cupertino",
    "region": "US-CA",
    "country": "US",
    "postalCode": "95014",
    "formatted": "One Apple Park Way, 95014 Cupertino, US-CA, US"
  },
  "directParent": {
    "lei": null,
    "name": null,
    "exception": "NATURAL_PERSONS"
  },
  "ultimateParent": {
    "lei": null,
    "name": null,
    "exception": "NATURAL_PERSONS"
  },
  "successorLei": null,
  "wikidataId": "Q312",
  "wikidataLinkedBy": "lei",
  "description": "American multinational technology company based in Cupertino, California",
  "website": "https://apple.com/",
  "industry": [
    "software industry",
    "consumer electronics industry",
    "digital distribution"
  ],
  "inception": "1976-04-01",
  "employees": {
    "value": 164000,
    "asOf": "2022"
  },
  "revenue": {
    "amount": 416161000000,
    "currency": "USD",
    "asOf": "2025"
  },
  "stockExchanges": [
    {
      "exchange": "Nasdaq",
      "ticker": "AAPL"
    }
  ],
  "isin": [
    "US0378331005"
  ],
  "ceo": "John Ternus",
  "country": "United States",
  "countryCode": "US",
  "logoUrl": "https://commons.wikimedia.org/wiki/Special:FilePath/Apple_logo_black.svg",
  "social": {
    "linkedin": "https://www.linkedin.com/company/apple",
    "x": "https://x.com/Apple",
    "facebook": "https://www.facebook.com/apple",
    "instagram": "https://www.instagram.com/apple/",
    "youtube": "https://www.youtube.com/channel/UCE_M8A5yxnLfW0KghEeajjw",
    "github": "https://github.com/apple",
    "tiktok": "https://www.tiktok.com/@apple"
  },
  "wikipediaUrl": "https://en.wikipedia.org/wiki/Apple_Inc.",
  "candidates": [],
  "warnings": [],
  "sources": {
    "gleif": "https://api.gleif.org/api/v1/lei-records/HWUPKR0MPOU8FGXBT394",
    "wikidata": "https://www.wikidata.org/wiki/Q312"
  },
  "gleifDataDate": "2026-10-19T00:00:00Z",
  "charged": true,
  "checkedAt": "2026-10-19T09:21:49.223Z"
}
```

</details>

## Use it from code

Set your token in the `APIFY_TOKEN` environment variable.

**Node.js** ([`apify-client`](https://docs.apify.com/api/client/js/))

```js
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('far003/company-profile-lei-wikidata').call({
    "companies": [
        "HWUPKR0MPOU8FGXBT394"
    ]
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

**Python** ([`apify-client`](https://docs.apify.com/api/client/python/))

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("far003/company-profile-lei-wikidata").call(run_input={
    "companies": ["HWUPKR0MPOU8FGXBT394"]
})
items = client.dataset(run["defaultDatasetId"]).list_items().items
print(items)
```

## Pricing

Pay per result — see the current price on the Store page.

## Data source & licence

Everything about the legal entity comes from GLEIF, the Legal Entity Identifier registry (CC0 licence: https://www.gleif.org/en/meta/lei-data-terms-of-use). Everything about the business comes from Wikidata (structured data CC0: https://www.wikidata.org/wiki/Wikidata:Licensing). Logos and images are not downloaded: `logoUrl` is only a link to the file page on Wikimedia Commons, where each file has its own licence. This Actor is not affiliated with, or endorsed by, GLEIF or the Wikimedia Foundation.

## Support

Open an issue in this repository or use the Issues tab on the Store page.

## Licence

The documentation and examples in this repository are released under the MIT licence (see `LICENSE`). The Actor itself is proprietary and runs on the Apify platform.
