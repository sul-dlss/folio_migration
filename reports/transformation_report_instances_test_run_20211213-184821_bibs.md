# Bibliographic records transformation results   
Time Run: 2021-12-13T17:49:13.563504   
<br/>Data errors preventing records from being migrated are marked **FIX BEFORE MIGRATION**. The library is advised to clean up these errors in the source data.<br/><br/> The sections related to field counts and mapping results are marked **REVIEW**. These do not indicate errors preventing records from being migrated, but may point to data anomalies or in the mappings. The library should review these to make sure that the numbers are what one would expect, knowing the source data. Is this the expected number of serials? Is this the expected number of cartographic materials?
   
## General statistics    
A list of general counterts to outline the transformation as a whole.    
<details><summary>Click to expand all 7 things</summary>     
   
Measure | Count   
--- | ---:   
Lines written to identifier map | 1   
Records in file before parsing | 2   
Records successfully parsed from MARC21 | 1   
Records successfully transformed into FOLIO objects | 1   
Records with encoding errors - parsing failed | 1   
Total number of Tags processed | 37   
</details>   
   
## Record status (leader pos 5)    
Library action: **Consider fixing d-values before migration**<br/>An overview of the Record statuses (Leader position 5) present in your source data.    Pay attention to the number of occurrences of the value 'd'. These d's are expressing that they are deleted, and the records might not work as expected in FOLIO. Consider marking them as suppressed in your current system and export them as a separate batch in order to have them suppressed in FOLIO. Allowed values according to the MARC standard are a,c,d,n,p    
<details><summary>Click to expand all 2 things</summary>     
   
Measure | Count   
--- | ---:   
n | 1   
</details>   
   
## HRID Handling    
There are two ways of handling HRIDs. The default behaviour is to take the current 001 and move that to a new 035. This will also emerge as an Identifier on the Inventory Instances. The 001 and Instance HRID will be generated from the HRID settings in FOLIO. The second option is to maintain the 001s in the records, and also add this as the Instance HRID    
<details><summary>Click to expand all 4 things</summary>     
   
Measure | Count   
--- | ---:   
Added 035 from 001 | 1   
Created HRID using default settings | 1   
Values in 003: DE-He213 | 1   
</details>   
   
## Mapped identifier types    
Library action: **REVIEW** <br/>The created FOLIO instances contain the following Identifier type values. The library should review the total number for each value against what they would expect to see mapped.    
<details><summary>Click to expand all 4 things</summary>     
   
Measure | Count   
--- | ---:   
020 -> ISBN | 1   
024 -> Other Standard Identifier | 1   
035 -> System Control Number | 2   
</details>   
   
## Non-numeric tags in records    
Library action: **REVIEW** <br/>Non-numeric tags may indicate locally defined fields.    
<details><summary>Click to expand all 2 things</summary>     
   
Measure | Count   
--- | ---:   
FMT | 1   
</details>   
   
## Incomplete entity mapping adding entity    
**NO ACTION REQUIRED** <br/>This is a coding anomaly that FSE will look into.  <br/>Usually, the library does not have to do anything about it.<br/> One thing to look at is if there are many repeated subfields or unexpected patterns of subfields in the table.    
<details><summary>Click to expand all 2 things</summary>     
   
Measure | Count   
--- | ---:   
020 a:has_value ->>-->> identifiers identifierTypeId:'False' - value:'False'   | 1   
</details>   
   
## Mapped classification types    
    
<details><summary>Click to expand all 3 things</summary>     
   
Measure | Count   
--- | ---:   
Dewey | 1   
LC | 1   
</details>   
   
## Mapped contributor name types    
Library action: **REVIEW** <br/>The created FOLIO instances contain the following Name type values. The library should review the total number for each value against what they would expect to see mapped.    
<details><summary>Click to expand all 3 things</summary>     
   
Measure | Count   
--- | ---:   
100 -> Personal name | 1   
710 -> Corporate name | 1   
</details>   
   
## Contributor type mapping    
Library action: **REVIEW** <br/>The created FOLIO instances contain the following Contributor type values. The library should review the total number for each value against what they would expect to see mapped.    
<details><summary>Click to expand all 2 things</summary>     
   
Measure | Count   
--- | ---:   
Contributor type code Author found for $4 "aut" (aut)) | 1   
</details>   
   
## Mapped publisher role from Indicator2    
Publication Role, taken from the code in Ind2    
<details><summary>Click to expand all 2 things</summary>     
   
Measure | Count   
--- | ---:   
264 ind2 1->Publication | 1   
</details>   
   
## Instance format ids handling (337 + 338))    
    
<details><summary>Click to expand all 3 things</summary>     
   
Measure | Count   
--- | ---:   
Successful match  - "cr"->computer -- online resource | 1   
Successful match  - cr->computer -- online resource | 1   
</details>   
   
## Mapped note types    
Library action: **REVIEW** <br/>The created FOLIO instances contain the following Note type values.  <br/>The library should review the total number for each value against what they would expect to see mapped.    
<details><summary>Click to expand all 3 things</summary>     
   
Measure | Count   
--- | ---:   
505 (Formatted Contents Note) -> Formatted Contents Note | 1   
520 (Summary) -> Summary | 1   
</details>   
   
## Resource Type Mapping (336, 008)    
Library action: **REVIEW** <br/>The created FOLIO instances contain the following Instance type values. The library should review the total number for each value against what they would expect to see mapped.    
<details><summary>Click to expand all 2 things</summary>     
   
Measure | Count   
--- | ---:   
336$b text mapped from txt | 1   
</details>   
   
## Matched Modes of issuance code    
Library action: **REVIEW** <br/>The created FOLIO instances contain the following Mode of issuace values. The library should review the total number for each value against what they would expect to see mapped.    
<details><summary>Click to expand all 2 things</summary>     
   
Measure | Count   
--- | ---:   
single unit -- 9d18a02f-5897-4c31-9106-c9abb5c7ae8b | 1   
</details>   
   
## Language codes in records    
A breakdown of language codes occuring in the records. Purely informational.    
<details><summary>Click to expand all 2 things</summary>     
   
Measure | Count   
--- | ---:   
eng | 1   
</details>   

## Mapped FOLIO fields
<details><summary>Click to expand field report</summary>     

FOLIO Field | Mapped | Unmapped  
--- | --- | ---:  
_version | 0 (0%) | 1  
alternativeTitles | 0 (0%) | 1  
catalogedDate | 0 (0%) | 1  
classifications.classificationNumber | 2 (200%) | 0  
classifications.classificationTypeId | 2 (200%) | 0  
contributors.contributorNameTypeId | 2 (200%) | 0  
contributors.contributorTypeId | 2 (200%) | 0  
contributors.contributorTypeText | 2 (200%) | 0  
contributors.name | 2 (200%) | 0  
contributors.primary | 1 (100%) | 0  
electronicAccess | 0 (0%) | 1  
holdingsRecords2 | 0 (0%) | 1  
hrid | 1 (100%) | 0  
id | 1 (100%) | 0  
identifiers.identifierTypeId | 4 (400%) | 0  
identifiers.value | 4 (400%) | 0  
indexTitle | 1 (100%) | 0  
instanceFormats | 0 (0%) | 1  
instanceTypeId | 1 (100%) | 0  
matchKey | 0 (0%) | 1  
metadata.createdByUserId | 1 (100%) | 0  
metadata.createdDate | 1 (100%) | 0  
metadata.updatedByUserId | 1 (100%) | 0  
metadata.updatedDate | 1 (100%) | 0  
modeOfIssuanceId | 1 (100%) | 0  
natureOfContentTermIds | 0 (0%) | 1  
notes.instanceNoteTypeId | 2 (200%) | 0  
notes.note | 2 (200%) | 0  
previouslyHeld | 0 (0%) | 1  
publication.dateOfPublication | 1 (100%) | 0  
publication.place | 1 (100%) | 0  
publication.publisher | 1 (100%) | 0  
publication.role | 1 (100%) | 0  
publicationFrequency | 0 (0%) | 1  
publicationPeriod | 0 (0%) | 1  
publicationRange | 0 (0%) | 1  
series | 0 (0%) | 1  
source | 1 (100%) | 0  
sourceRecordFormat | 0 (0%) | 1  
statisticalCodeIds | 0 (0%) | 1  
statusId | 0 (0%) | 1  
statusUpdatedDate | 0 (0%) | 1  
tags | 0 (0%) | 1  
title | 1 (100%) | 0  
</details>   

## Mapped Legacy fields
<details><summary>Click to expand field report</summary>     

Legacy Field | Present | Mapped | Unmapped  
--- | --- | --- | ---:  
001 | 1 (100.0%) | 1 (100%) | 0  
003 | 1 (100.0%) | 0 (0%) | 1  
005 | 1 (100.0%) | 0 (0%) | 1  
006 | 1 (100.0%) | 0 (0%) | 1  
007 | 1 (100.0%) | 0 (0%) | 1  
008 | 1 (100.0%) | 1 (100%) | 0  
020 | 1 (100.0%) | 1 (100%) | 0  
024 | 1 (100.0%) | 1 (100%) | 0  
035 | 2 (200.0%) | 2 (200%) | 0  
050 | 1 (100.0%) | 1 (100%) | 0  
082 | 1 (100.0%) | 1 (100%) | 0  
100 | 1 (100.0%) | 1 (100%) | 0  
245 | 1 (100.0%) | 1 (100%) | 0  
250 | 1 (100.0%) | 1 (100%) | 0  
264 | 1 (100.0%) | 1 (100%) | 0  
300 | 1 (100.0%) | 1 (100%) | 0  
336 | 1 (100.0%) | 1 (100%) | 0  
337 | 1 (100.0%) | 0 (0%) | 1  
338 | 1 (100.0%) | 1 (100%) | 0  
347 | 1 (100.0%) | 0 (0%) | 1  
505 | 1 (100.0%) | 1 (100%) | 0  
520 | 1 (100.0%) | 1 (100%) | 0  
650 | 10 (1000.0%) | 10 (1000%) | 0  
655 | 1 (100.0%) | 1 (100%) | 0  
710 | 1 (100.0%) | 1 (100%) | 0  
773 | 1 (100.0%) | 0 (0%) | 1  
FMT | 1 (100.0%) | 0 (0%) | 1  
</details>   
