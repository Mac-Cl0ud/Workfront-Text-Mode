# Adobe Workfront Text Mode Repository
This repository is intended to store text mode (reports) and formulas (calculated fields) for users of Adobe Workfront.
<hr>

## Display an Image in a Report

```
displayname=Link Project
image.name=Link Project
image.valuefield=URL
link.linkproperty.0.name=projectID
link.linkproperty.0.value=ID
link.lookup=link.edit
link.page=/view
link.valuefield=objCode
link.valueformat=val
textmode=true
type=image
valueformat=
```
> [!NOTE]
> Insert the URL for the image into the URL field in the project details, then use the above code
to replace a column in text mode. Any image linked via the URL in the project details will show up in the column. Images appear in their actual resolution so try to use small images!
This example is for projects, but applies to any object with a URL in the system details.
https://github.com/Mac-Cl0ud/Workfront-Text-Mode/blob/main/display_image_in_report
<hr>

# Truncate Last Note and Dsplay as a Tweet
Use this code in a report column to display the last note, limited to 140 characters, with name of commenter and date.

```
valueexpression=IF(LEN({lastNote}.{noteText})>140,CONCAT(SUBSTR({lastNote}.{noteText},0,139),"... (open for more) -- ",{lastNote}.{owner}.{name}," on ",{lastNote}.{entryDate}),IF(LEN({lastNote}.{noteText})>0,CONCAT({lastNote}.{noteText}," -- ",{lastNote}.{owner}.{name}," on ", {lastNote}.{entryDate}))) 
valueformat=HTML 
displayname=Last Note 
width=250 
textmode=true
querysort=lastNote:entryDate 
usewidths=true
```
https://github.com/Mac-Cl0ud/Workfront-Text-Mode/blob/main/last-note-tweet
