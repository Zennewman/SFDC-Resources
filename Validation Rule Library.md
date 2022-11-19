---
title: Validation Rule Library
updated: 2022-08-08 17:30:34Z
created: 2022-08-01 15:46:05Z
author: Zen Newman
---

### Limit record ownership change

Limits ownership change based on who is currently the owner and which profile the user attempting to make the change has.

```
ISCHANGED(OwnerId)&&
OwnerId = "0053i000002gvY2" &&
$Profile.Name <> "System Administrator" &&
$Profile.Name <> "Bitrise Sales Manager" &&
$Profile.Name <> "Bitrise SDR"
```

### Prevent field overwrite once populated

`AND(NOT(ISBLANK(PRIORVALUE(LeadSource))),ISCHANGED(LeadSource))`

### Restrict who can mark opportunity as closed won

Limit stage updates by profile type. Includes validation override

```
TEXT(StageName) = 'Closed Won' &&
$Profile.Name <> 'System Administrator' &&
$Profile.Name <> 'Sales Administrator' &&
$Profile.Name <> 'Sales Engineer' &&
Validation_Override__c = FALSE
```

### Validate presence of opportunity contacts roles

validates the presence of records on a junction object (in this case the opportunity contact role). Requires the presence of a custom field showing true indicating those records exist. That field must be populated by a flow that queries for those records. The below flows are also used to validate the presence of each role individually as well as in aggregate using the same method.

```
TEXT(StageName) = "Closed Won" &&
Has_Contact_Roles__c = FALSE &&
$Profile.Name <> "System Administrator" &&
$User.BypassValidationRule__c = FALSE
```

Flow used to populate Has_Contact_Roles__c
![[_resources/image 4.png]]
![[image 1 1 1.png]]
### Require value in one field based on the value in another

When a drop down is populated with a specific value, require a value in a second field. Overrides build in for System Administrators as well as a system wide override field for use with automations.

```

TEXT( POC_Type__c ) = 'Guided' && ISBLANK(SE__c) && $Profile.Name <> "System Administrator" &&

$User.BypassValidationRule__c = FALSE && Validation_Override__c = FALSE
```

### End date before start date

Validates that a CPQ quote's end date is later than it's start date.

`IF(AND( NOT(ISNULL(SBQQ__EndDate__c)), SBQQ__EndDate__c < SBQQ__StartDate__c), TRUE, null)`

### Prevent field overwrite once populated

`AND(NOT(ISBLANK(PRIORVALUE(LeadSource))),ISCHANGED(LeadSource))`
