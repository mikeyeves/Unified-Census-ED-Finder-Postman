# Unified Census ED Finder — Postman Collection

Postman collection for the **[Unified Census ED Finder](https://stevemorse.org/census/unified.html)** by Stephen P. Morse & Joel D. Weintraub. It turns a historical street address into a U.S. census **Enumeration District (ED)** for 1870–1950, so you can go straight to the right census pages.

> **Unofficial.** These are the undocumented endpoints the finder's own web page calls. They return JSONP-wrapped HTML and may change without notice. Not affiliated with or endorsed by the authors — please keep request volume low and credit stevemorse.org.

## Import
Postman → **Import** → paste:
`https://raw.githubusercontent.com/mikeyeves/Unified-Census-ED-Finder-Postman/main/Unified_Census_ED_Finder.postman_collection.json`

## Workflow
Set the collection variables `census_year` and `state`, then run in order:

| # | Request | Endpoint | Output |
|---|---|---|---|
| 1 | List counties | `/census/unifiedcounties.php?year&state` | County names |
| 2 | List cities | `/census/unifiedcities.php?year&state&county` | City codes (e.g. `MA` = Manhattan) |
| 3 | List streets | `/census/unifiedstreets.php?year&state&city` | Street names + the EDs each passes through |
| 4 | **Find EDs** | `/census/unified.php?…&street1…street5` | EDs containing **all** listed streets → saved to `{{ed}}` |
| 5 | View census pages | `/census/reelframes.html` (1880–1930) | Open in browser |
| 6 | ED description | `/ed/ed2_pre.php` (pre-1930) or `/ed/ed2.php` | Open in browser |
| 7 | NARA scans (1940/1950) | National Archives Catalog API | Page images; needs `nara_api_key` |

Each request has a script that parses the response into a readable table (**Visualize** tab) and, for step 4, saves the ED into variables for steps 5–7.

**Tips**
- Use street names exactly as step 3 shows them (e.g. `12th W`, `7th Ave`, `Greenwich Ave`).
- Enter the house's street **plus both cross streets** to narrow the result to one ED.
- Street indexes differ by year, and some streets are missing in some years.

## Worked example (preloaded)
Block bounded by W 11th St, W 12th St and 7th Ave, Manhattan (today's Greenwich Lane):

| Year | Streets | ED |
|---|---|---|
| 1910 | `11th W` + `12th W` + `7th Ave` | **30-160** |
| 1950 | same | **31-87** → NARA item [308013370](https://catalog.archives.gov/id/308013370) |

## Related collections
- [Federal Register & National Archives Catalog APIs](https://github.com/mikeyeves/US-Federal-Register-National-Archives-Catalog-APIs)
- [Hebcal Jewish Calendar APIs](https://github.com/mikeyeves/Hebcal-Jewish-Calendar-APIs)
