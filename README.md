# EC2 Monitoring and Remediation System – ServiceNow Implementation
The EC2 Remediation System is a ServiceNow-powered workflow that automatically detects, alerts, and resolves failing AWS EC2 instances affecting Netflix’s streaming infrastructure. Its purpose is to minimize incident response time while seamlessly integrating with DevOps processes through Slack and AI Search.

The solution eliminates delays in identifying EC2 instance failures by automating the following:
- Incident creation for failed instances
- AI-driven knowledge retrieval
- Slack notifications with actionable remediation steps
- One-click manual remediation through a streamlined UI Action
- Detailed logging for auditing and post-incident review

## Architecture Diagram
![](https://github.com/CodeWithLuwam/EC2-remediation-system/blob/main/Diagram.png?raw=true)

## 1. Application Setup <br>
- ServiceNow Studio allowed me to create and manage my application, keeping all components packaged together under its scope.
![](https://github.com/CodeWithLuwam/EC2-remediation-system/blob/main/Images/ServiceNow%20Studio.png?raw=true) 

## 2. Custom Tables
  - EC2 Instance
![](https://github.com/CodeWithLuwam/EC2-remediation-system/blob/main/Images/EC2%20Instance%20table.png?raw=true)
  - Remediation Log
![](https://github.com/CodeWithLuwam/EC2-remediation-system/blob/main/Images/Remediation%20Log%20table.png?raw=true)


## 3. AWS Integration Configuration
  - Reference the alias instead of hardcoding the connection or credential
![](https://github.com/CodeWithLuwam/EC2-remediation-system/blob/main/Images/Connection%20and%20Credential.png?raw=true)

  - Endpoint the integration will talk to
![](https://github.com/CodeWithLuwam/EC2-remediation-system/blob/main/Images/URL%20Integration%20will%20talk%20to.png?raw=true) 

  - To authenticate a connection
![](https://github.com/CodeWithLuwam/EC2-remediation-system/blob/main/Images/Basic%20Auth%20Credentials%20-%20AWS%20Integration%20Server%20.png?raw=true)

## 4. UI Actions Configuration - Trigger EC2 Remediation
- The `trigger_EC2_Remediation` client script executes from the form, passes the current record’s `sys_id` to the `EC2RemediationHelper` Script Include (via GlideAjax), notifies the user of success/failure, and refreshes the form to show the updated Remediation Log.
![](https://github.com/CodeWithLuwam/EC2-remediation-system/blob/main/Images/UI%20Action%20-%20Trigger%20EC2%20Remediation.png?raw=true)

## Script Include - EC2RemediationHelper
- The `triggerRemediation` function in `EC2RemediationHelper` takes an EC2 instance `sys_id`, finds the record, pulls the AWS connection details, and sends a REST API request to restart the instance. It logs the entire process to the Remediation Log and returns a JSON response with the result and metadata.
![](https://github.com/CodeWithLuwam/EC2-remediation-system/blob/main/Images/Script%20Include%20-%20EC2RemediationHelper.png?raw=true)

## 5. Flow Designer Workflow
![](https://github.com/CodeWithLuwam/EC2-remediation-system/blob/main/Images/Workflow.png?raw=true)

- Workflow Trigger<br>
![](https://github.com/CodeWithLuwam/EC2-remediation-system/blob/main/Images/Workflow%20-%20Trigger%20and%20Condition.png?raw=true)<br>

- Workflow Action 1 <br>
![](https://github.com/CodeWithLuwam/EC2-remediation-system/blob/main/Images/Workflow%20-%20Action.png?raw=true) <br>

- Workflow Action 2 <br>
![](https://github.com/CodeWithLuwam/EC2-remediation-system/blob/main/Images/Workflow%20-%20Action%20Input.png?raw=true)

 
## 6. Knowledge Base Integration
- Created KB article “Trigger EC2 Remediation” with keywords for AI Search discoverability.
![](https://github.com/CodeWithLuwam/EC2-remediation-system/blob/main/Images/Knowledge%20Base%20-%20IT.png?raw=true) <br>

## 7. Testing and Validation
- EC2 Remediation System alert <br>
![](https://github.com/CodeWithLuwam/EC2-remediation-system/blob/main/Images/Slack%20EC2%20Remediation%20alert.png?raw=true)
