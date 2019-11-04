# importicd

SAS Macro for facilitating handling of ICD-codes, especially complex cases with multiple ICD-versions from multiple countries, and with multiple different groupings. 

Originally created for SCANDAT2 but can be easily adapted to be used with other datasets.

The repository includes
* importicd3.sas - the latest version of the macro
* importicd_template - excel template used for the macro
* importicd3_examples - some examples of the macro

This macro requires the use of the excelfile template importicd_template.xlsx
It allows differentiation between SE and DK ICD-codes.;
![Image overview of Importicd](https://github.com/SCANDAT/importicd/blob/master/importicd.png)
It generates the following;
````
groupname.			- a SAS format with the group name for the corresponding group number;
groupdescription.		- a SAS format with the group description for the corresponding group number;
&where 				- a global SAS macro variable to be used in a proc SQL statement (example below);
&groupif			- a global SAS macro variable to be used in a data step (example below);
import_icd			- SAS dataset with all the ICD codes, including country and ICD-version vars;
````


Dependencies: modified versions of CODEPICKER by Klaus Rostgaard (included in the .sas file)

## Syntax

````
%macro importicd(

filepath			/*filepath of excelfile based on importicd_template.xlsx. E.g. "C:/documents/excel.xlsx") */
,icdtypes			/*icdtypes - format is e.g. 7SE for Swedish ICD7, or 8DK for Danish ICD8. Needs corresponding excelsheet with 'ICD' prefix* (included in template)*/
,output=import_icd		/*name of the output file*/
,formatname=group		/*name of the SAS formats name and description*/
,mode=passthrough		/*modes can be 'passthrough' or 'local'. If 'passthrough' the &where clause will use "substring()", whereas 'local' uses 'substr()*/
,diavar=b.diagnosis		/*name of the diagnosis variable in the proc.sql statement*/
,countryvar=a.country		/*name of the country variable in the proc.sql statement*/
,icdvar=b.icd			/*name of the icd variable in the proc.sql statement*/
);
```
