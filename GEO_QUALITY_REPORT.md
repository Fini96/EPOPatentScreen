# Geographic data-quality report

Semiconductor Patent Atlas (CNIPA & TIPO study). Applicant locations verified 2026-11-05. File: `data/applicant_locations.json` (one record per applicant ID, joined to the patent statistics by `applicant_id`).

## 1. Precision of applicant locations

| Precision | Institutional applicants | Share | Share of their applications | Private inventors |
|---|---:|---:|---:|---:|
| Exact site (organisation coordinates) | 591 | 4.0% | 6.8% | 0 |
| City (city-centre coordinates) | 8,718 | 58.8% | 75.5% | 0 |
| Province / state only | 2,475 | 16.7% | 7.5% | 0 |
| Country only (location unverified) | 2,721 | 18.4% | 9.5% | 274 |
| Unknown | 318 | 2.1% | 0.6% | 49 |
| **Total** | **14,823** | 100% | 100% | **323** |

Applicants drawn as individual map markers (exact or city): **9,309 of 14,823 institutional applicants (62.8%)**, accounting for 82.3% of their applications. Private inventors are deliberately kept at country level (no residential addresses were searched or used).

## 2. Sources and confidence (institutional applicants)

| Source | Applicants |
|---|---:|
| Registered applicant name (CNIPA record) + Wikidata city coordinates | 7,553 |
| none | 3,039 |
| Registered applicant name (CNIPA record) | 2,397 |
| USPTO patent records (PatentsView) | 1,222 |
| Wikidata | 591 |
| Manual web verification | 21 |

| Confidence | Applicants |
|---|---:|
| medium | 10,349 |
| n/a | 3,039 |
| high | 1,434 |
| low | 1 |

Confidence rules: *high* = organisation item matched uniquely in Wikidata, or ≥80% of ≥3 US grants give the same city, or two independent sources within 40 km, or a manually verified headquarters; *medium* = single automated source (e.g. city in the registered Chinese name, minority USPTO evidence, manual source without street address); *low* = sources disagree.

## 3. Automated checks

- **Country consistency**: 9,309 drawn points tested against Natural Earth 1:10m country polygons: **0 fall in a different country** than the applicant’s country (Hong Kong/Macau accepted for CN applicants).
- **Coastal points**: 135 city-centre points on coasts/islands fall just outside the generalised coastline; all lie within 11.8 km of their own country’s polygon.
- **Latitude/longitude order**: 0 points would only match their country with swapped axes (0 = order correct). MapLibre receives `[longitude, latitude]`.
- **No national centroids**: applicants known only to country or province level are not drawn as markers; they are shown as dashed group circles at a label point and listed as unverified. 1,114 distinct coordinates are in use.
- **Largest shared coordinates** (city centres; they fan out into individually selectable markers on click): Shenzhen (1,185), Shanghai (986), Suzhou (789), Beijing (623), Wuxi (329), Hangzhou (258), Chengdu (211), Nanjing (210).
- **Patent totals unchanged**: applicant application counts, family counts and types identical to the study data: **yes**; publication records identical: **yes** (99,546 records). 868 applicants with previously unknown country received the country of their verified location (this moves them from ‘unknown’ into a country in country statistics; no counts change).

## 4. Large and diverse countries

| Country | Applicants | Exact | City | Province | Country only | Distinct cities | Leading cities (applicants) |
|---|---:|---:|---:|---:|---:|---:|---|
| CN | 11,632 | 477 | 7,762 | 2,424 | 969 | 261 | Shenzhen 1237, Shanghai 1005, Suzhou 809, Beijing 678, Wuxi 335, Hangzhou 275 |
| US | 664 | 16 | 234 | 0 | 414 | 158 | San Jose 17, Santa Clara 12, Wilmington 6, Sunnyvale 6, Fremont 5, San Diego 5 |
| JP | 869 | 27 | 309 | 39 | 494 | 69 | Tokyo 156, Osaka 37, Kyoto 23, Kawasaki 9, Yokohama 9, Nagoya 6 |
| KR | 274 | 12 | 59 | 8 | 195 | 20 | Seoul 18, Daejeon 13, Hwaseong 4, Ulsan 4, Daegu 4, Suwon 3 |
| TW | 555 | 21 | 183 | 0 | 351 | 19 | Hsinchu 50, New Taipei 37, Taipei 28, Taoyuan 19, Taichung 14, Kaohsiung 12 |
| DE | 156 | 5 | 70 | 0 | 81 | 54 | Munich 9, Stuttgart 3, Hanau 3, Ludwigshafen 2, Jena 2, Dortmund 2 |
| IN | 2 | 0 | 0 | 0 | 2 | 0 |  |
| FR | 59 | 13 | 13 | 0 | 33 | 17 | Paris 4, Versailles 3, Grenoble 3, Annecy 2, Bernin 1, Blagnac 1 |
| GB | 60 | 5 | 13 | 1 | 41 | 14 | Manchester 3, London 3, Cambridge 1, Cambourne 1, South Yorkshire 1, Bristol 1 |
| NL | 22 | 2 | 10 | 0 | 10 | 9 | Veldhoven 2, Nijmegen 2, Eindhoven 2, Almere 1, Duiven 1, 's-Hertogenbosch 1 |

## 5. Spot checks of well-known applicants

| Applicant | Country | Location | Precision | Source |
|---|---|---|---|---|
| Samsung (incl. Display, SDI, SEMES) | KR | Suwon, Gyeonggi | city | [USPTO patent records (PatentsView)](https://patents.google.com/patent/US10057597) |
| TSMC | TW | Hsinchu | city | [USPTO patent records (PatentsView)](https://patents.google.com/patent/US10672866) |
| Applied Materials | US | Santa Clara, CA | city | [USPTO patent records (PatentsView)](https://patents.google.com/patent/US9257293) |
| Tokyo Electron | JP | Tokyo | city | [USPTO patent records (PatentsView)](https://patents.google.com/patent/US11062922) |
| SK hynix | KR | Icheon, Gyeonggi | city | [Manual web verification: Wikipedia (infobox: Headquarters "I](https://en.wikipedia.org/wiki/SK_Hynix) |
| CXMT (ChangXin) | CN | Hefei, Anhui | city | [Manual web verification: Wikipedia (infobox: Headquarters "H](https://en.wikipedia.org/wiki/ChangXin_Memory_Technologies) |
| Infineon | DE | Neubiberg, Bavaria | city | [USPTO patent records (PatentsView)](https://patents.google.com/patent/US8994943) |
| Micron | US | Boise, ID | city | [USPTO patent records (PatentsView)](https://patents.google.com/patent/US10614872) |
| Intel | US | Santa Clara, CA | city | [USPTO patent records (PatentsView)](https://patents.google.com/patent/US9344986) |
| ASML | NL | Veldhoven, North Brabant | city | [USPTO patent records (PatentsView)](https://patents.google.com/patent/US10580545) |
| ASM International | NL | Almere, Flevoland | city | [USPTO patent records (PatentsView)](https://patents.google.com/patent/US10876218) |
| SOITEC SILICON ON INSULATOR | FR | Bernin, Isère | city | [USPTO patent records (PatentsView)](https://patents.google.com/patent/US9583531) |
| imec | BE | Leuven, Flemish Brabant | city | [USPTO patent records (PatentsView)](https://patents.google.com/patent/US11069648) |
| JCET (incl. STATS ChipPAC) | CN | Jiangyin, Jiangsu | city | [Manual web verification: Wikipedia (infobox: Headquarters "J](https://en.wikipedia.org/wiki/JCET_(company)) |
| Resonac | JP | Tokyo | city | [Manual web verification: Wikipedia (infobox: Headquarters "T](https://en.wikipedia.org/wiki/Resonac) |
| Tsinghua University | CN | Beijing | exact | [Wikidata](https://www.wikidata.org/wiki/Q16955) |
| USTC | CN | Hefei, Anhui | exact | [Wikidata](https://www.wikidata.org/wiki/Q1074103) |
| ITRI | TW | Hsinchu | city | [USPTO patent records (PatentsView)](https://patents.google.com/patent/US9395072) |
| YMTC (Yangtze Memory) | CN | Wuhan, Hubei | city | [USPTO patent records (PatentsView)](https://patents.google.com/patent/US10423176) |
| Huawei (incl. HiSilicon) | CN | Shenzhen, Guangdong | city | [USPTO patent records (PatentsView)](https://patents.google.com/patent/US9654160) |

## 6. Subsidiaries are located independently

Each applicant is located from its own names; a parent’s headquarters is never copied to a subsidiary. Grouped applicants (documented study rules, e.g. Samsung incl. Display/SDI/SEMES) are placed at the verified group headquarters where checked, otherwise at the address of the group’s principal filing entity, and the record says which.

Separately listed entities of large groups keep their own locations:

- SEMICONDUCTOR MFG NORTH INTEGRATED CIRCUIT MFG BEIJING CO LTD → Beijing, CN (group “SMIC” → Shanghai, CN)
- SMIC INTEGRATED CIRCUIT NINGBO CO LTD → Ningbo, CN (group “SMIC” → Shanghai, CN)
- SEMICONDUCTOR MFG BEIJING CO LTD → Beijing, CN (group “SMIC” → Shanghai, CN)
- PEKING UNIVERSITY CHONGQING CARBON BASED INTEGRATED CIRCUIT RESEARCH INST → Chongqing, CN (group “Peking University” → Beijing, CN)
- PEKING UNIV CHONGQING CARBON BASED INTEGRATED CIRCUIT RESEARCH INSTITUTE → Chongqing, CN (group “Peking University” → Beijing, CN)
- SIEN SEMICONDUCTOR TECH SUZHOU CO LTD → Suzhou, CN (group “SiEn (Qingdao)” → Qingdao, CN)

Affiliated units of universities and academies (Chinese names such as 北京工业大学重庆研究院) are placed at the place named for the unit, not at the parent: 31 such units, e.g. 扬州大学扬州碳中和技术创新研究中心 → Yangzhou; 北京大学重庆碳基集成电路研究院 → Chongqing; 北京大学东莞光电研究院 → Dongguan; 北京大学重庆碳基集成电路研究院 → Chongqing; 西北工业大学深圳研究院 → Shenzhen. Where the unit's own place is not named, the parent's location is not used and the unit stays unverified (10 cases, e.g. 中国人民解放军军事科学院国防科技创新研究院; 中国人民解放军军事科学院国防科技创新研究院; 西湖大学光电研究院).

## 7. Applicants whose location could not be verified

5,837 applicants (incl. 323 private inventors) have no verified city-level location: 2,475 province only, 2,995 country only, 367 unknown. All remain in every statistic. The complete list is `data/unverified_locations.csv`; the 40 with the most applications:

| ID | Applicant | Type | Country | Precision | Applications | Note |
|---:|---|---|---|---|---:|---|
| 47 | Zhejiang Chuangxin IC | company | CN | region (Zhejiang) | 302 |  |
| 54 | Sony | company | JP | region (Kanagawa) | 249 | USPTO city field "Kanagawa" is a province/state |
| 84 | CanSemi (Yuexin) | company | CN | country | 163 |  |
| 107 | HKC | company | CN | country | 125 |  |
| 132 | Hubei Jiufengshan Laboratory | research institute | CN | region (Hubei) | 101 |  |
| 135 | Hubei Xingchen Technology | company | CN | region (Hubei) | 99 |  |
| 139 | JIANGSU LEUVEN INSTR CO LTD | company | CN | region (Jiangsu) | 97 | USPTO city field "Jiangsu" is a province/state |
| 141 | Adeia | company | US | country | 95 |  |
| 143 | GBA Institute of IC & Systems | research institute | CN | region (Guangdong) | 92 |  |
| 155 | ROBERT BOSCH CO LTD | company | DE | country | 84 | USPTO address country CN differs from dataset country DE |
| 164 | Guangdong Xinyueneng | company | CN | region (Guangdong) | 80 |  |
| 173 | JIANGSU LEADMICRO NANOMETER TECH CO LTD | company | CN | region (Jiangsu) | 74 |  |
| 177 | Hikstor | company | CN | region (Zhejiang) | 69 |  |
| 187 | HUBEI SINOPHORUS ELECTRONIC MATERIALS CO LTD | company | CN | region (Hubei) | 65 |  |
| 193 | ZHEJIANG AOSHOU MATERIAL TECH CO LTD | company | CN | region (Zhejiang) | 63 |  |
| 194 | Yongjiang Laboratory | research institute | CN | country | 62 |  |
| 202 | NAT CT ADVANCED PACKAGING CO LTD NCAP CHINA | company | CN | country | 58 |  |
| 205 | JIANGXI MTC SEMICONDUCTOR CO LTD | company | CN | region (Jiangxi) | 57 |  |
| 208 | CANON TOKKI CORP | company | JP | country | 56 |  |
| 209 | HITACHI ENERGY CORP | company | – | unknown | 56 |  |
| 211 | SOULBRAIN CO LTD | company | KR | region (Gyeonggi-do) | 56 | USPTO city field "Gyeonggi-do" is a province/state |
| 222 | LG ELECTRONICS INC | company | JP | country | 54 | USPTO address country KR differs from dataset country JP |
| 224 | THE 55TH RESEARCH INSTITUTE OF CHINA ELECTRONICS TECH GROUP CORPORATION | company | CN | country | 54 |  |
| 226 | TOYOTA MOTOR CORP | company | JP | region (Aichi) | 54 | USPTO city field "Aichi" is a province/state |
| 232 | JIANGSU PANGU SEMICONDUCTOR TECH CO LTD | company | CN | region (Jiangsu) | 52 |  |
| 240 | PHYTIUM TECHNOLOGY CO LTD | company | CN | country | 51 |  |
| 251 | ICLEAGUE TECH CO LTD | company | CN | country | 49 |  |
| 254 | JIANGSU TIANXIN MICRO SEMICONDUCTOR EQUIPMENT CO LTD | company | CN | region (Jiangsu) | 48 |  |
| 260 | INFORMATION ENGINEERING UNIV OF PEOPLES LIBERATION ARMY OF CHINA | university | CN | country | 47 |  |
| 262 | EBERSOLIC INC | company | US | country | 46 |  |
| 264 | EV GROUP E THALLNER GMBH | company | AT | country | 46 | USPTO city "St. Florian am Inn,  AT" could not be geocoded consistently |
| 265 | HUBEI JIANGCHENG CHIP PILOT PRODUCTION SERVICES CO LTD | company | CN | region (Hubei) | 46 |  |
| 267 | FUTURE VISION TECHNOLOGIES INC | company | JP | country | 45 |  |
| 270 | TOKUYAMA CORP | company | JP | country | 45 | USPTO addresses inconsistent (top city Yamaguchi only 49%) |
| 272 | ABSOLICS INC | company | US | country | 44 |  |
| 276 | NO 24 RES INST CETC | company | CN | country | 44 |  |
| 279 | AVAGO TECHNOLOGIES GENERAL IP | company | US | country | 43 | USPTO address country SG differs from dataset country US |
| 282 | SHENGJISHENG KOREA SEMICONDUCTOR TECH CO LTD | company | KR | country | 43 |  |
| 288 | CN ELECT TECH NO 13 RES INST | company | CN | country | 42 |  |
| 290 | NIPPON ELECTRIC GLASS CO | company | JP | region (Shiga) | 42 | USPTO city field "Shiga" is a province/state |

## 8. Map geometry

The previous map drew country outlines from Overture Maps polygons that had been simplified per country with a coarse tolerance and rounded to 0.01°; neighbouring borders were simplified independently, which produced jagged edges, slivers and gaps, and some multipart geometries lost parts. The map now uses MapLibre GL JS with an OpenStreetMap-based vector basemap (OpenFreeMap, no API key) and Natural Earth 1:10m country polygons (rounded to 0.001°, ~100 m) for selection and shading; if the online basemap is unreachable, Natural Earth 1:10m borders, provincial boundaries and cities shipped with the site are used. Zooming runs from world level to individual cities (zoom 0.8–17).
