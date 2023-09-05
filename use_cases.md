# Architectural drivers
The section captures significant requirements driving the solution architecture and road map. The requirements which are not influencing the solution architecture in major ways and low level requirement details and scenarios are typically excluded from this section and can be found in the requirement specification or the product backlogs.
## Major features
The section enumerates solution major features.



|   | Description | 
| --- | ----------- | 
| F-1 | Secure data access, transmission, and storage protected from the unauthorized access | 
| F-2 | Access from the mobile devices and desktop browsers for data entry | 
| F-3 | Application will offer an administrative view for busines process (calculations) governance. |  
| F-4 | Application will offer an administrative view for data entry UI governance. |  
| F-5 | Integration with existing federal tax submission solution (export) | 



## Use cases
[[use_cases.drawio]]
### Use Case Tax filing

#### Element Catalog

|  # | Name | Description |
| --- | ----------- | --- |
| ACT-1 | User | A business user of the system  |
| UC-1 | Enter data to forms | User enters his financial data on  |
| UC-2 | login to the application | User logs to the system and gains access to previously entered data | 
| UC-3 | trigger taxes calculations | User send his data to the calculatoin engine, and retrieves calculated forecast | 
| UC-4 | export entered data to federal system   | | 



### Use Case Calculation Engine Governance

#### Element Catalog

|  # | Name | Description |
| --- | ----------- | --- |
| ACT-2 | User | An administrative user | 
| UC-5 | define calculation rules | Tax calculation (and it's steps) is defined a set of rules, which is maintained and versioned by the administrator. Must define it's own coherence rules.| 
| UC-6 | define forms for data entry | For the Calculation Engine data, appropriate data must be gathered, and therefore corresponding data forms must be defined. The same versioning must be used as for calculation, and validation of rules must also include corresponding entry forms. | 

