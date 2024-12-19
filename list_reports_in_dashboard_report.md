##Add this text mode to a DASHBOARD report to list reports and calendars in the dashboard##

column.2.displayname=Reports & Calendars  
column.2.listdelimiter=<br>
column.2.listmethod=nested(portalTabSections).lists
column.2.sharecol=true
column.2.textmode=true
column.2.type=iterate
column.2.valueexpression={internalSection}.{name}
column.2.valueformat=HTML
column.3.displayname=Calendars
column.3.listdelimiter=<br>
column.3.listmethod=nested(portalTabSections).lists
column.3.textmode=true
column.3.type=iterate
column.3.valueexpression={calendarPortalSection}
column.3.valueformat=HTML
