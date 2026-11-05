# Methodology and data-quality note

## Dataset

* **Source**: Google Patents Public Datasets on BigQuery (`patents-public-data.patents.publications`), queried 3–4 Nov 2026.
* **Scope**: invention patents (kind A/B) whose *first* publication at CNIPA (CN) or TIPO (TW) falls on or after 1 Nov 2024, with at least one CPC/IPC code in the semiconductor/quantum core scope (H10D, H10B, H10N60, H10P, H10W, H01L 21/23/25/27/29, G06N10, B82Y10, G06F30/39) or a quantum keyword in the title/abstract. Utility models are excluded.
* **Coverage**: 99,546 applications (CN 80,062, TW 19,484). Latest publication in the data: CN 8 Sep 2026, TW 21 Jun 2026. Recent months are incomplete because of the ~18-month publication lag.
* **Not included**: publications at other offices (the separate EP study is not part of this dashboard).

## Counting

* **Applications**: each application is counted once, at its first publication (later A/B publications of the same application are merged). In this dataset “publications” and “applications” are the same unit.
* **Families**: distinct DOCDB family IDs. A family with members at both CNIPA and TIPO counts once (89,159 families overall).
* **Co-applicants**: *full counting* credits an application to every co-applicant, so applicant totals sum to more than the dataset total. *Fractional counting* (switch in the filter bar) credits 1/n to each of n applicant groups. Dataset, country and applicant-type totals always count each application once.
* **Technology**: 65 categories in 12 groups, assigned from CPC/IPC patterns and English/Chinese text rules. An application can belong to several categories; totals never count it twice. Applications that match no category are not forced into one.

## Applicants and types

* Names are Google Patents’ harmonised names, cross-checked with the original-language name. 155 documented rules group subsidiaries and name variants under a parent (e.g. Samsung Electronics, Samsung Display, SDI, SEMES → Samsung). Everything else stays a separate applicant.
* Types: company, university, research institute, private inventor, other/unknown, from the grouping table or name tokens (大学/University, 研究所/Institute, company forms). **Startups cannot be identified from patent data**, so no applicant is labelled a startup; that category is shown but empty.
* **Private inventors** are natural persons named as *applicants* (not inventors on institutional filings), found by name pattern; 20 organisations wrongly caught by the pattern were reclassified by hand. Name variants are not merged. Filings alone, with institutions, or with other individuals are distinguished in each profile.

## Geography

Three modes, chosen in the dashboard:

* **A · Applicant location** (default): applicant headquarters or organisational site.
* **B · Inventor location**: inventor countries from TIPO records only (CNIPA records carry none); country level; inventors are not treated as applicants.
* **C · Filing jurisdiction**: offices where the family has members (EP, US, JP, KR, WO, CN, TW were queried). EP (regional) and WO (PCT) are shown separately and never treated as an origin.

### Applicant locations (`data/applicant_locations.json`)

The patent records contain no applicant addresses for these offices, so every applicant was located from external, citable sources (verified 5 Nov 2026). Sources, in order of preference:

1. **Wikidata** (mid-2025 snapshot on BigQuery): the organisation’s own item, matched by harmonised or original-language name, restricted to organisation classes and to the applicant’s country. Its coordinate location (P625) is used as the exact site. The live Wikidata service and its headquarters property (P159) were not reachable from the build environment, so P159 was not used.
2. **USPTO applicant addresses** (PatentsView, US grants 2012–2021): the city given by the applicant on its own US patents, if at least half of its grants agree; geocoded with Wikidata/Natural Earth and checked against state and country.
3. **Registered Chinese name**: Chinese legal names state the administrative division of registration (合肥晶合… → Hefei; …（上海）有限公司 → Shanghai). Affiliated units (北京工业大学重庆研究院) are placed at the unit’s own place, never at the parent’s.
4. **Manual web verification** for the largest groups and unresolved cases (Wikipedia infobox headquarters, company filings).

Precision levels: *exact* (organisation coordinates), *city* (city centre), *region* (province only), *country* (location unverified), *unknown*. Only exact and city locations are drawn as individual markers. Province- and country-level applicants are shown as dashed group circles at a label point and listed as unverified; they are never placed at a national centroid as if it were their address. Private inventors are kept at country level and no residential information was searched.

Grouped applicants are placed at the verified group headquarters where checked, otherwise at the address of the group’s principal filing entity; the record states which.

## Quality checks

See `GEO_QUALITY_REPORT.md`: precision by applicant type and country, sources and confidence, point-in-country test (0 mismatches), coordinate order check, shared-coordinate stacks, unchanged patent totals, subsidiaries, and the list of unverified applicants.

## Limitations

* City-level points are city centres; the registered city in a Chinese name may differ from the operating site; USPTO addresses date from grants up to 2021.
* Many CNIPA applicants’ countries are inferred from their earliest priority office; a foreign company filing first in China would appear as Chinese.
* 37% of institutional applicants (about 18% of their applications) could not be located below province or country level.
* Most frequent CPC/IPC groups and the sample publications in each profile are stored without filters.
