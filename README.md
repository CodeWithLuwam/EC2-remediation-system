# EC2 Monitoring and Remediation System – ServiceNow Implementation
1. Custom Tables:
  - EC2 Instance
![](https://github.com/CodeWithLuwam/EC2-remediation-system/blob/main/Images/EC2%20Instance%20table.png?raw=true)
  - Remediation Log
![](https://github.com/CodeWithLuwam/EC2-remediation-system/blob/main/Images/Remediation%20Log%20table.png?raw=true)
2. UI Actions- Trigger EC2 Remediation
  - Added as a form button on EC2 Instance REcords
  - Executes client-side script using GlideAjax

3. Script Include - EC2RemediationHelper
  - Handles outbound REST requests via the Connection & Credential Store (CCS).
  - Reads instance ID, calls the AWS Integration Server, and inserts log entries.

4.  Flow Designer Workflow
  - Trigger: When EC2 Instance status updates to OFF.
  - Actions:
    - Create log record
    - Run AI Search against Knowledge Base
    - Post Slack notification via webhook
 
5. Knowledge Base Integration
  - Created KB article “EC2 Remediation when OFF” with keywords for AI Search discoverability.
 Connection

6. Connection & Credential Store
  - Alias: AWS Integration Server C C Alias
  - Connection: Host + base path /api/v1/queue/start
  - Credential: Basic Auth (admin user)
