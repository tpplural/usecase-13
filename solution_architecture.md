# Solution architecture 
The section Solution Architecture is primary for the Architecture Vision document. It defines and reasons about the solution architecture design based on the architecturally significant requirements and constraints identified in the section Architectural Drivers.

## Big Picture

The section includes a list of architectural views covering the designed solution along with the context it runs in on the high level.

### Solution Context

[[big_picture.draw.io]] Illustration  

|Name | Description | 
| --- | ----------- |
| Federal Tax System | External system responsible for accepting validated data from a tax payer | 
| Backend Application | Responsible for handling the user input process, validates the input, handles state of the data entry process, delegates calculation to  Calculation Engine. Also responsible for generating the views |
| Calculation Engine | Responsible for calculation of the financial data, available via an API Gateway |
| Web Application | Responsible for handling user input and data validation. Communicates with the Backend Application via REST API. | 
| Mobile Client | Device used to access the Web Application |
| Desktop Client | Device used to access the Web Application |

### Application Deployment

[[application_deployment.drawio]] Illustration  

The cloud based part of the solution is decomposed into several parts documented below combining several standard architectural patterns applicable to the highly loaded cloud based SaaS applications: Load Balancer, Storage, and Autoscaler. The subsection resoning provides detailed discussion of these choices.

|# | Description | 
| --- | ----------- |
| Webapp Instance | responsible for rendering the user forms, as well calculated data. Relies on Backend Application to retrieve the forms content | 
| Backend Application | Node.js application responsible for communication with client, rendering dynamical views, and handling communication with Calculation Engine (via API Gateway) and persistent storage. | 
| Federal Tax System | External system, where income data is exported, after being validated | 
| Lambda functions | means for calculating the financial information, orchestrated by Calculation Engine, chosen for their scaling capabilities |
| Redis instance | Stores information about running calculations (to block parallel executions), results are also written to it |
| API Gateway | Entry point for the Calculation Engine |
| Amazon RDS |Stores calcution results for users, their status (partial/validated/sent), and data forms definitions (versioned)  |
|Amazon Cognito |provides an identity store for users of the application | 
| Active Directory | Database and a set of services that connects users with the resources required |
| Amazon Cloudwatch | collects and visualizes real-time logs, metrics, and event data |

#### Behavior 
[[tax_information_entry_workflow.drawio]]

The diagram shows basic workflow for entering fiscal data into the system. User logs into the system, and after being authenticated enters his data on presented forms. The forms are generated serverside (SSR - Server Side Rendering) which allows for the forms (fields, validation logic) to be fully customizable by the administrator. The definitions (versioned) are loaded from the database. This allows for a multi-step data entry (wizard), where data gathered in each step is dependent on previous. 
Each step (same effect is triggered by some preconfigured fields) is concluded by a call to the Calculation Engine. To avoid parallel executions for the same user (which may cause incostencies), calculations calls are queued - with simple mechanism where a Redis instance is storing information about running calculations. Each subsuquent call is being made with current data from form, as well the results from latest calculations.
Results of calculations are stored in an RDS instance, which persists user data between sessions, and is used for export to (external) federal tax system. 


### Development Technology Stack

|  Name | Version | Description |
| --- | ----------- | --- |
| Java | 17 | Java is used in implementation of calculation engine(Java part) |
| NodeJS | 18.12.0 | Used in the implementation of the webapp backend |
| Spring Framework | 6.0 | Used in implementation of calculation engine(Java part) | 
| Angular  | 15.0.2 | Framework for implementation of the web application using SSR Pattern | 
| Log4j 2  | 2.19.0 |Logging framework for Java applications |