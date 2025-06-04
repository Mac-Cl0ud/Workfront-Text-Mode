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

## User Information on a User Report
Add this textmode to a user report or view to get the users Title, Manager, Access Level, Home Group, Home Team, and Job role in a single column. Update colors to your preference.

```
column.2.width=280
column.2.value=<div style=background:#e3e1fc"><font color=000000><b>Title: </b></font>
column.2.shortview=false
column.2.displayname=User Information
column.2.sharecol=true
column.2.usewidths=true
column.2.textmode=true
column.2.valueformat=HTML
column.3.linkedname=direct
column.3.descriptionkey=title
column.3.valuefield=title
column.3.namekey=title.abbr
column.3.textmode=true
column.3.sharecol=true
column.3.usewidths=true
column.3.shortview=false
column.3.valueformat=HTML
column.4.shortview=false
column.4.value=<br><font color=000000><b>Manager: </b></font>
column.4.usewidths=true
column.4.sharecol=true
column.4.textmode=true
column.4.valueformat=HTML
column.5.link.lookup=link.view
column.5.link.valuefield=manager:objCode
column.5.link.linkproperty.0.valueformat=int
column.5.link.linkproperty.0.name=ID
column.5.link.linkproperty.0.valuefield=manager:ID
column.5.link.valueformat=val
column.5.querysort=manager:name
column.5.sharecol=true
column.5.textmode=true
column.5.shortview=false
column.5.linkedname=manager
column.5.usewidths=true
column.5.valuefield=manager:name
column.5.descriptionkey=manager
column.5.namekey=manager
column.5.valueformat=HTML
column.6.sharecol=true
column.6.usewidths=true
column.6.textmode=true
column.6.value=<br><font color=000000><b>Access Level: </b></font>
column.6.valueformat=HTML
column.6.shortview=false
column.7.usewidths=true
column.7.namekey=accesslevel
column.7.sharecol=true
column.7.shortview=false
column.7.linkedname=accessLevel
column.7.descriptionkey=accesslevel
column.7.textmode=true
column.7.querysort=accessLevel:name
column.7.valueformat=HTML
column.7.valuefield=accessLevel:displayName
column.8.value=<hr><div style=background:#f6f5ff"><font color=000000><b>Home Group: </b></font></b>
column.8.displayname=Primary Associated Fields
column.8.textmode=true
column.8.shortview=false
column.8.sharecol=true
column.8.usewidths=true
column.8.valueformat=HTML
column.9.textmode=true
column.9.listsort=nested(homeGroup).string(name)
column.9.valuefield=homeGroup:name
column.9.descriptionkey=homegroup
column.9.usewidths=true
column.9.sharecol=true
column.9.shortview=false
column.9.namekey=homegroup
column.9.linkedname=homeGroup
column.9.valueformat=HTML
column.10.usewidths=true
column.10.textmode=true
column.10.shortview=false
column.10.value=<br><font color=000000><b>Home Team: </b></font></b>
column.10.valueformat=HTML
column.10.sharecol=true
column.11.textmode=true
column.11.valuefield=homeTeam:name
column.11.linkedname=homeTeam
column.11.valueformat=HTML
column.11.shortview=false
column.11.descriptionkey=hometeam
column.11.sharecol=true
column.11.namekey=hometeam
column.12.value=<br><font color=000000><b>Primary Job Role: </b></font></b>
column.12.sharecol=true
column.12.usewidths=true
column.12.valueformat=HTML
column.12.textmode=true
column.12.shortview=false
column.13.valueexpression=CONCAT({role})
column.13.namekey=roleID
column.13.linkedname=direct
column.13.textmode=true
column.13.valueformat=HTML
column.13.querysort=roleID
```
For you eagle eyes, you might be wondering why Primary Role uses "CONCAT" in the valueexpression. Well, that's because Workfront was doing what Workfront does sometimes and for some reason the standard "Job Role" field would not display when pulled into a shared column. Go figure. The upshot of this is that you can pull in the percent allocation to the role if you are so inclined:
```
valueexpression=CONCAT({role}," (",{timePercentage},"%)")
```
