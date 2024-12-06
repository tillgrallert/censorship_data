---
title: "Readme: censorship_data"
author: Till Grallert
date: 2024-12-05 
lang: en
tags:
    - censorship
    - Ottoman Empire
    - press
---

This repository contains all my data on Ottoman press censorship in Bilād al-Shām and beyond between the mid-nineteenth century and the end of World War I.

The main data file is `xml/censorship-levant_biblstruct.TEIP5.xml`

# structure of this repository

The repository is structured by type and serialisation formats:

- `csv/`
    - `censorship-levant.csv`: derivative of the main source of truth, `censorship-levant_biblstruct.TEIP5.xml`, generated through an [XSLT transformation](../censorship_tools/xslt/convert_tei-to-csv.xsl).
    - derivate files that aggregate data by periodical and year. These are generated with R scripts found in [censorship_tools](../censorship_tools/r/).
- `html/`
- `plots/`: outputs of R scripts found in [censorship_tools](../censorship_tools/r/).
- `xml/`: contains only the main source of truth, `censorship-levant_biblstruct.TEIP5.xml`, from which all other subsets and serialisations derive

# to do

- [ ] merge information into the OpenArabicPE/Sihafa project

# data model

The data model follows the Open Arabic Periodical Editions and Jarāʾid projects. The main item is a periodical, encoded in TEI/XML with `<tei:biblStruct>`. Titles are linked to the main authority file through `@ref` on `<title>`, e.g. `<title level="j" ref="jaraid:bibl:t1r2506 oape:bibl:1799 wiki:Q124971839" resp="#xslt">Shams al-Ittiḥād</title>`


## events of relevance

Each periodical (`<tei:biblStruct>`) carries an event note following the example below:

```xml
<note type="events">
     <listEvent>
         <event type="censorship" subtype="permit" source="some">
             <label>received permit</label>
         </event>
         <event type="censorship" subtype="warning" source="some">
             <label>received warning</label>
         </event>
         <event type="censorship" subtype="suspension" source="some">
             <label>suspended</label>
         </event>
         <event type="censorship" subtype="ban" source="some">
             <label>banned from publication</label>
         </event>
     </listEvent>
 </note>
```

All computational analysis depends on attribute values on `<event>`