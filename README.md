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

## Truncate Last Note and Display as a Tweet
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

## Display Attached Document Names & Links in Project Report
Use this code to display a list of attached documents in a project, task, or issue report or view.

```
displayname=Documents
listdelimiter=<br>
listmethod=nested(documents).lists
textmode=true
type=iterate
valueexpression=CONCAT({name},".",{currentVersion}.{ext}," - https://DOMAIN.my.workfront.com/document/view?ID=",{ID})
valueformat=HTML
```

## Display Upcoming Time-off in User Report
Add this column to a User report or view to display future time off dates for each user.

```
displayname=Upcoming Time Off
listdelimiter=<br>
listmethod=nested(reservedTimes).lists
type=iterate
valueexpression=IF({endDate}>$$TODAY,CONCAT({startDate}," - ",{endDate}," "))
valueformat=HTML
```
https://github.com/Mac-Cl0ud/Workfront-Text-Mode/blob/main/upcoming_time_off_in_user_report

## Friendly URL

Add this column to a report to display a friendly version of a URL captured in a custom field.

```
displayname=COLUMN HEADER
link.url=DE:Custom_Field
linkedname=
namekey=view.relatedcolumn
namekeyargkey.0=
namekeyargkey.1=Custom_Field
querysort=DE:Custom_Field
shortview=false
valueexpression=IF(ISBLANK({DE:Custom_Field}),"","Click Here")
valuefield=Custom_Field
valueformat=HTML
```
Credit: [Adobe Experience League](https://experienceleaguecommunities.adobe.com/t5/workfront-questions/text-mode-friendly-url-displaying-when-url-hasn-t-been/m-p/515660])
