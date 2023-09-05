# Quality Attribute Scenarios
A Quality Attribute Scenario is an unambiguous and testable requirement for one or more Solution Quality Attributes such as Performance, Usability, Maintainability and others. The scenario consists of six parts: Source of Stimulus, Stimulus, Environment, Artifact, Response, testable and accurate Response Measure.
This section lists and prioritizes the scenarios pertinent to the designed solution.

|  # | QA | Scenario | Related to
| --- | ----------- | --- | --- |
| QA-1 | Security (security of data in the system) | Financial information is stored in a secure location, and accessible only by authorized users | UC-2
| QA-2 | Usability| data entry is guided by a series of form (wizard)| UC-1 
| QA-3 | Compatibility | Data must be exported to federal tax system after validation| UC-4
| QA-4 | Functional suitability | system allows for precalcuton of tax obligations | UC-3
| QA-5 | Efficiency/Performance | System must be able to scale out at the end of the fiscal year| UC-3
| QA-5 | Relialability | System must be available for 99% of time | UC-1, UC-3
| QA-5 | Maintainability | caluclation rules, as well as the input form must be changeable without system rebuild/downtime| UC-5, UC-6
| QA-5 | Portability | The system can be used on different client patforms (mobile client support)| UC-2
