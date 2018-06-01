# mdcoverage

This repository contains sample SFDX source files and data files for the enhanced Metadata Coverage Report.

To use:

- Create a SFDX scratch org:  
      sfdx force:org:create -f config/project-scratch-def.json -a testmdcoverage
- Push source into scratch org:  
      sfdx force:source:push -u testmdcoverage
- Open scratch org: 
      sfdx force:org:open -u testmdcoverage
      
The source files contain a sample app called "MD Coverage", 2 custom reports (MDSummaryRpt1 and MDSummaryRpt2), and 2 custom objects (MD_Type, WorkItem).

To view the MD Coverage app, go to App Launcher in the scratch org, and select "MD Coverage" app.
You should see 3 tabs:  Reports, MD_Types, WorkItems
Until you import or create data, there will be no records available to view.  

To import data:

- Go to MD_Types tab.  Click Import.
- Select MD_Types custom object to import to
- Select Add new and update existing records
     - Match by: Name
     - Which User field in your file designates record owners?:  None
     - Trigger workflow rules and processes?:  false
- Select CSV file.  Choose data/report_053018.csv.  Next.
- Map fields:
     - MD_Type Name -> Metadata Type
     - MDAPI -> Metadata API
     - Source Tracking -> Source Tracking (force:source:push/pull)
     - Unlocked Packaging -> Unlocked Packaging
     
- Start Import (Next)
- Repeat steps above for data/gaps_051418.csv

- Go back to the MD Coverage app, and select WorkItems tab.  Click Import.
- Select WorkItems custom object to import to
- Select Add new and update existing records
     - Match by: Name
     - Which User field in your file designates record owners?:  None
     - Which MD_Type field in your file specifies the Master/Detail relationship?:  MD_Type Name
     - Trigger workflow rules and processes?:  false
- Select CSV file.  Choose data/MD_by_Theme_GUS_053018.csv.  Next. 
- Map fields:
     - WorkItem Name -> Work ID
     - URL Id -> Internal ID
     - Type -> Type
     - Work Item Status -> Status
     - Work Item Scheduled Release -> Scheduled Build Name
     - Work Item Description -> Subject
     - KI_Hits -> KI Reporting Customers
     - KI Id -> Known Issue ID
     - KI Link with count -> Known Issue Link
     - Work Item OwningTeam -> Scrum Team Name
     - <unmapped> -> Theme:Theme Name
     - MD_Type -> MD Type
  
After the data is imported, you should be able to view data in the Reports (MDSummaryRpt1 and MDSummaryRpt2), and view details on the individual records for MD_Types and WorkItems  
