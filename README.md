## How to use this playbook to programatically create Change Requests with linked CTasks ?

Pre-Requisites:
- Ansibe-Core


Install the Ansible Collection for ServiceNow ITSM
```bash
 ansible-galaxy collection install -r requirements.yml
```


Populate the Change Request and corresponding CTasks as follows

```yaml
# vars/change_request.yml

- description: Network Upgrade
  short_description: Upgrade Core Network
  state: new
  type: normal
  requested_by: Change.Manager
  assigned_to: Change.Manager
  category: Software
  service_offering: Blackberry
  configuration_item: BlackBerry Desktop Manager
  impact: low
  urgency: low
  assignment_group: Change Management
  justification: | 
    Justification
    Here
  implementation_plan: Implementation Here
  risk_impact_analysis: Risk and Impacted Analysis Here
  backout_plan: Backout Plan Here
  test_plan: Lower Env Test Plan
  validation_plan: Product Validation Plan
  expected_start: "2024-05-14 13:37:34"
  expected_end: "2024-05-14 20:37:34"
  ctasks:
    - short_description: Router Configuration
      description: Router Configuration
      type: implementation
      state: open
      configuration_item: Bond Trading
      assignment_group: Software
      assigned_to: beth.anglin
      expected_start: "2024-05-14 14:00:00"
      expected_end: "2024-05-14 20:00:00"
    - short_description: Switch Firmware Upgrade
      description: Upgrade all switches to firmware v12.3.
      type: implementation
      state: open
      configuration_item: Bond Trading
      assignment_group: Software
      assigned_to: beth.anglin
      expected_start: "2024-05-14 14:00:00"
      expected_end: "2024-05-14 20:00:00"

```
Run the playbook

```bash
 ansible-playbook playbooks/create_change_request.yml
``` 
