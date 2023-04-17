# Glottolog ISBN Extraction

The goal with this information would be to compare access points from the perspective of scholars and librarians. This would also give an interesting insight into how the LCSH terms are used as well as LCC terms/IDs on Linguistic and language based resources. By comparing these data sources we learn or gain insight into what scholars consider important as opposed to what librarians consider important and we can further consider how information services meet consumer goals. This repo contains the 20,880 ISBNs that I extracted from the bibliography of the Glottolog version 4.7. 

* Activities performed by: Hugh Paterson III
* Glottolog version used: 4.7
* Date of Extraction: 17 April 2023
* Source file: glottolog_source.bib.zip [61.4MB]
* Source file format: bibTeX
* Source location: https://glottolog.org/meta/downloads
* Method of Extraction: text mining via Linux Command line tools 
* Result Files: 
  * ISBNs: Glottolog-ISBN-Final.txt
  * OCLC IDs: glottolog-OCLCnumbers.txt

## Methods

The following methods were loosely followed... There was a lot of one-off search and replace within a text-editor. Ultimatly I added a prefix to many ISBNs so that I could get the last 1000 or so. `ISBN10 0` -->  `ISBN-0`. ISBNs occured in a variety of fields, including ISSN, Title, notes (various), ISBN, citation, abstract, etc. A global search for `ISBN` was refined to filter and clean out the noise. Spaces and minus signs were removed. 

Some commands used were:

$ unzip glottolog_source.bib.zip

$ grep -i "ISBN" glottolog.bib > ISBN.txt

$ cat ISBN.txt | sort > ISBN-sorted.txt

$ cat ISBN-sorted.txt | sort -u > ISBN-sorted-u.txt

$ tr ' ' '\n' < title-test-1-minus-minuses-expeirment.txt | sort | uniq

$ tr ' ' '\n' < title-test-1-minus-minuses-expeirment.txt | sort | uniq | grep ISBN

$ tr ' ' '\n' < title-test-1-minus-minuses-expeirment.txt | sort | uniq | sed -nr '/^.{6,}$/p'

$ tr ' ' '\n' < Glottolog-ISBNs-Extracted.txt | sort | uniq > Glottolog-ISBN-Final.txt


## Follow-up actions
The ISBNs are sent to OCLC requesting MARC records for the matching ISBNs and then those records will be overlayed with the bibtex records. Analysis will ensue.
