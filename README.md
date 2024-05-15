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

- description: Migrate Dynatrace OneAgents to SaaS
  short_description: Dynatrace OneAgents Migration to SaaS
  state: new
  type: normal
  requested_by: Monitoring.Admin
  assigned_to: Monitoring.Team
  category: Monitoring
  service_offering: Dynatrace SaaS
  configuration_item: Dynatrace OneAgents
  impact: high
  urgency: high
  assignment_group: Monitoring Management
  justification: |
    The migration to Dynatrace SaaS will enhance monitoring capabilities, improve scalability, and reduce maintenance overhead. 
    It will also provide access to the latest features and updates.
  implementation_plan: |
    1. Review existing Dynatrace OneAgent configurations.
    2. Create migration plan and timeline.
    3. Communicate migration plan to stakeholders.
    4. Begin migration by moving non-critical OneAgents first.
    5. Validate OneAgent performance on SaaS.
    6. Gradually migrate remaining OneAgents.
    7. Decommission on-premise Dynatrace environment.
    8. Monitor performance post-migration.
  risk_impact_analysis: |
    Risk:
    - Possible downtime during migration.
    - Potential configuration issues post-migration.
    
    Impact:
    - High impact due to potential monitoring disruptions affecting all services.
  backout_plan: |
    1. Revert OneAgent configurations to point to the on-premise Dynatrace environment.
    2. Restore previous monitoring settings if any issues are detected.
  test_plan: |
    1. Test the migration process with a subset of OneAgents.
    2. Conduct performance and connectivity tests on the SaaS environment.
    3. Validate monitoring data accuracy and functionality post-migration.
  validation_plan: |
    1. Confirm OneAgent data and configuration integrity post-migration.
    2. Verify full monitoring coverage and functionality.
    3. Monitor for any issues and resolve promptly.
  expected_start: "2024-06-15 08:00:00"
  expected_end: "2024-06-15 18:00:00"
  ctasks:
    - short_description: Review OneAgent Configurations
      description: Review and document current Dynatrace OneAgent configurations.
      type: preparation
      state: open
      configuration_item: Dynatrace OneAgents
      assignment_group: Monitoring Management
      assigned_to: bob.smith
      expected_start: "2024-06-15 08:00:00"
      expected_end: "2024-06-15 09:00:00"
    - short_description: Migrate Non-Critical OneAgents
      description: Migrate non-critical Dynatrace OneAgents to the SaaS environment.
      type: implementation
      state: open
      configuration_item: Dynatrace OneAgents
      assignment_group: Monitoring Management
      assigned_to: alice.johnson
      expected_start: "2024-06-15 09:00:00"
      expected_end: "2024-06-15 12:00:00"

      ...
      ...
      ...
```
Run the playbook

```bash
 ansible-playbook playbooks/create_change_request.yml
```

> [!NOTE]  
> For each new Change Request, create a new Git branch

> [!TIP]
> Ability to cleanup and destroy the Change Requests created is work in progress
