# Migration Repo template
This repo is a template repository for the files needed for migrating Inventory data from a source system into FOLIO 

TLDR; Create a new private repository based on this template. Clone it and then run create_folder_structure.sh 

# FOLIO Inventory data migration process
This template plays a vital part in a process together with other repos allowing you to perform bibliographic data migration from a legacy ILS into FOLIO. For more information on the process, head over to the linked repos below.
In order to perform migrations according to this process, you need to clone the following repositories:   
* [MARC21-to-FOLIO](https://github.com/FOLIO-FSE/MARC21-To-FOLIO)
* [service_tools](https://github.com/FOLIO-FSE/service_tools)
* [migration_repo_template](https://github.com/FOLIO-FSE/migration_repo_template)


# Mapping files
The repo contains the following mapping files in the Mapping files folder.
There is a web tool that helps you crate the mapping files for certain objects available at https://data-mapping-file-creator.folio.ebsco.com/data_mapping_creation

## What file is needed for what objects?
File\Process | Bibs->Instances | Holdings (from MARC/MFHD) | Holdings (from item tsv/csv) | Items  | Open Loans  | Users   
------------ | ------------- | ------------- | ------------- | ------------- | ------------- | -------------   
marc-instance-mapping-rules.json  | yes | no | no | no |   no    |   no
mfhd_rules.json  | no | yes | no | no |  no   |   no
item_mapping.json  | no | no | no | yes |  no   |   no
holdings_mapping.json  | no | no | yes |  no   |   no
locations.tsv  | no | yes | yes | yes |  no   |   no
temp_locations.tsv.optional*  | no | no | no | optional |  no   |   no
material_types.tsv  | no | no | no |  yes   |   no
loan_types.tsv  | no | no | no | yes |  no   |   no
temp_loan_types.tsv.optional*  | no | no | no | optional |  no   |   no
call_number_type_mapping.tsv  | no | no | optional | optional |  no   |   no
statcodes.tsv  | no | no | optional | optional |  no   |   no
item_statuses.tsv | no | no | no | optional    |  no   |   no
post_loan_migration_statuses.tsv | no | no | no | no    |  optional  |   no
patron_types.tsv | no | no | no | no    |  no  |   yes
user_mapping.json** | no | no | no | no    |  no  |   yes

\* remove the .optional file ending to let the scripts know you want these mappings enabled.   
\*\* Currently, the user_mapping file name needs to reflect the name of the user data file it maps from.
## marc-instance-mapping-rules.json
These are the mapping rules from MARC21 bib records to FOLIO instances. The rules are stored in the tenant, but it is good practice to keep them under version control so you can maintain the customizations as the mapping rules evolve.For more information on syntax etc, read the [documentation](https://github.com/folio-org/mod-source-record-manager/blob/master/RuleProcessorApi.md).

## mfhd_rules.json
This file is built out according to the [mapping rules for bibs](https://github.com/folio-org/mod-source-record-manager/blob/master/RuleProcessorApi.md). The conditions are different, and not well documented at this point. Look at the example file and refer to the mappinrules documentation 

## holdings_mapping.json
Just as the item_mapping.json and the user mapping files, these files are esiest to create using the [data-mapping-file-creator tool](https://data-mapping-file-creator.folio.ebsco.com/data_mapping_creation)
You base the mapping on the same item export as you use for the items.

## item_mapping.json
This is a mapping file for the items. The process assumes you have the item data in a CSV/TSV format. 
The structure of the file is dependant on the the column names in the TSV file. For example, if you have a file that looks like this:
... | Z30_BARCODE | Z30_CALL_NO | Z30_DESCRIPTION |  ... 
------------ | ------------- | ------------- | ------------- | -------------
 ... | 123456790 | Some call number | some note  | ...
 


Your map should look like this:
```
...
{
    "folio_field": "barcode",
    "legacy_field": "Z30_BARCODE",
    "value":"",
    "description": ""
},
{
    "folio_field": "itemLevelCallNumber",
    "legacy_field": "Z30_CALL_NO",
    "value":"",
    "description": ""
}, 
{
    "folio_field": "notes[0].itemNoteTypeId",
    "legacy_field": "Z30_DESCRIPTION",
    "value": "c7bc292c-a318-43d3-9b03-7a40dfba046a",
    "description": ""
},
{
    "folio_field": "notes[0].staffOnly",
    "legacy_field": "Z30_DESCRIPTION",
    "value": false,
    "description": ""
},
{
    "folio_field": "notes[0].note",
    "legacy_field": "Z30_DESCRIPTION",
    "value": false,
    "description": ""
},
...
```
The resulting FOLIO Item would look like this:
```
{
	...
	"barcode": "123456790",
	"itemLevelCallNumber": "Some call number"
	"notes":[{
			"staffOnly": false,
			"note": "some note",
			"itemNoteTypeId": "c7bc292c-a318-43d3-9b03-7a40dfba046a"			
		}],
	...
}
```
### Default fields
All mapping files (locations.tsv, material_types.tsv, locations.tsv etc) have a mechanism that allows you to add * to legacy fields in a row, and add the default value from folio in the folio_code/folio_name column. If the mapping fails, the script will assign this value to the records created. Good practice is to have migration-specific value for defaults to be able to locate the records in FOLIO


## locations.tsv
These mappings allow for some complexity. These are the mappings of the legacy and FOLIO locations. The file must be structured like this:
 folio_code | legacy_code | Z30_COLLECTION 
------------ | ------------- | -------------
 AFA | AFAS | AFAS   
 AFA  |  * |  *    

 
The legacy_code part is needed for both Holdings migratiom. For Item migration, the source fields can be used (Z30_COLLECTION in this case). You can add as many source fields as you like for the Items

## material_types.tsv
These mappings allow for some complexity. The first column name is fixed, since that is the target material type in FOLIO. Then you add the column names from the Item export TSV. For each column added, the values in them must match. At least one value per column must match. Se loan_types.tsv for complex examples
 folio_name | Z30_MATERIAL 
------------ | ------------- 
 Audiocassette | ACASS
 Audiocassette | *

## loan_types.tsv
These mappings allow for some complexity. The first column name is fixed, since that is the target loan type in FOLIO. Then you add the column names from the Item export TSV. For each column added, the values in them must match. At least one value per column must match

 folio_name | Z30_SUB_LIBRARY | Z30_ITEM_STATUS 
------------ | ------------- | -------------
 Non-circulating | UMDUB | 02
 Non-circulating | * | *   

## call_number_type_mapping.tsv
These mappings allow for some complexity eventhough not needed. 
 folio_name | Z30_CALL_NO_TYPE 
------------ | -------------
Dewey Decimal classification | 8
Unmapped | *   

## statcodes.tsv
In order to map one statistical code to the FOLIO UUID, you need this map, and the field mapped in the item_mappings.json. These mappings allow for some complexity even though not needed. This mapping does not allow for default values. Any record without the field will not get one assigned.
 folio_code | Z30_STAT_CODE 
------------ | -------------
married_with_children | 8
happily_ever_after | 9

## item_statuses.tsv	
The handling of Item statuses is a bit of a project of its own, since not all statuses in legacy systems will have their equivalents in FOLIO. This mapping allows you to point one legacy status to a FOLIO status. If not status map is supplied, the status will be set to available.
legacy_code | folio_name 
------------ | -------------
checked_out | Checked out
available | Available
lost | Aged to lost

## post_loan_migration_statuses.tsv
This is not yet a mapping file per se, but it is used to substitute the values in the next_item_status column in the legacy open loans file.
Leave the statuses you do not want the loans migration process to migrate empty and replace the legacy statuses you want to apply with the correct FOLIO ones.

# Example Records
In the [example records folder](https://github.com/FOLIO-FSE/migration_repo_template/tree/main/example_files), you will find example source records and example results from after a transformation
## Result files
The following table outlines the result records and their use and role
 File | Content | Use for 
------------ | ------------- | ------------- 
folio_holdings.json | FOLIO Holdings records in json format. One per row in the file | To be loaded into FOLIO using the batch APIs
folio_instances.json | FOLIO Instance records in json format. One per row in the file | To be loaded into FOLIO using the batch APIs
folio_items.json |FOLIO Item records in json format. One per row in the file | To be loaded into FOLIO using the batch APIs
holdings_id_map.json | A json map from legacy Holdings Id to the ID of the created FOLIO Holdings record | To be used in subsequent transformation steps 
holdings_transformation_report.md | A file containing various breakdowns of the transformation. Also contains errors to be fixed by the library | Create list of cleaning tasks, mapping refinement
instance_id_map.json | A json map from legacy Bib Id to the ID of the created FOLIO Instance record. Relies on the "ILS Flavour" parameter in the main_bibs.py scripts | To be used in subsequent transformation steps 
instance_transformation_report.md | A file containing various breakdowns of the transformation. Also contains errors to be fixed by the library | Create list of cleaning tasks, mapping refinement
item_id_map.json | A json map from legacy Item Id to the ID of the created FOLIO Item record | To be used in subsequent transformation steps 
item_transform_errors.tsv | A TSV file with errors and data issues together with the row number or id for the Item | To be used in fixing of data issues 
items_transformation_report.md | A file containing various breakdowns of the transformation. Also contains errors to be fixed by the library | Create list of cleaning tasks, mapping refinement
marc_xml_dump.xml | A MARCXML dump of the bib records, with the proper 001:s and 999 fields added | For pre-loading a Discovery system.
srs.json | FOLIO SRS records in json format. One per row in the file | To be loaded into FOLIO using the batch APIs

