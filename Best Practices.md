# GPO Best Practices
Collection of rules for the creation and the handling of Active Directory Group Policy Objects.

## Motivation
Even in the age of Cloud Computing, GPOs are an essential component for the configuration management and security management of on-premises Active Directory domains. The creation and management of GPOs gives the administrator many options to achieve the desired goal, which is why it is particularly important that there are rules for the creation and usage of GPOs. The GPO technology has many functions such as Inheritance, Blocking, ACLs, Group or WMI filters that allow you to quickly create an environment that is no longer maintainable or difficult to find errors. The saying applies here again: less is more.

## The Rules
The best practices here are collected in six categories:

+ Names
+ Metadata
+ Test
+ Handling
+ Composition
+ General

### Definition
    A GPO Setting is the triple consisting of (GPO Path, GPO Name, GPO Value).

### (N) Name-Rules
    (N1) GPO names MUST follow a naming convention.
    (N2) Microsoft GPOs SHALL NOT be renamed.
    (N3) GPO names and descriptions must be written in English.
    (N4) The GPO SHOULD have a descriptive name.
    (N5) If a GPO makes a functional or individual setting, the name of the GPO SHOULD indicate whether something is enabled/disabled or allowed/disallowed using that GPO. In this case, the words Enable(d)/Disable(d) or Allow(ed)/Disallow(ed) SHOULD be used in GPO names.
    (N6) A GPO with security settings MUST have the SECURITY flag in its name.
    (N7) A GPO with basic settings MUST have the BASELINE flag in its name.
    
### (M) Metadata-Rules
    (M1) Each GPO used in production MUST contain a description that adequately describes the purpose of it. For this purpose we use the GPO Comment field.
    (M2) The description SHOULD contain the following attributes:
| Tag | Environment | Usage | Description |
| ---- | ---- | ---- | ---- |
| Description | Production | Mandatory | Short and understandable description of the purpose of the GPO |
| | Test | Optional ||
| Owner | Production | Mandatory | Responsible for the productive GPO or for the test (Type: Mail) |
|   | Test | Mandatory ||
| ReviewPeriod | Production | Optional | ReviewPeriod (Type: Integer) is the period in months until the next review MUST be performed. For Test-GPOs, the value **PERMANENT** is allowed here to indicate that the Test-GPO should remain permanent.|
| | Test | Mandatory |
| LastReviewDate | Production | Optional | LastReviewDate (Type: YYYY-MM-DD) is the date of the last review of the GPO.|
| | Test | Mandatory | |
| LastChangedBy | Production | Mandatory | Author who made the last change (Type: Mail \| Account \| Fullname).|
| | Test | Mandatory ||
| ChangeID | Production | Mandatory | ID of a Change-, ISMS- or any other ticket system.|
| | Test | Optional ||
    (M3) Production GPOs that include security settings must have the Owner, ReviewPeriod and LastReviewDate tags to schedule a security review.

:exclamation: If an attribute Tag is not used, the Tag should have the value **NA**.   
:exclamation: The attribute Tags ReviewPeriod and LastReviewDate must appear together.

### (T) Test-Rules
    (T1) Changing productive or creating new GPOs MUST follow a defined test procedure.
    (T2) If there is no independent test environment, GPO tests SHOULD be carried out in a special Test-OU with a dedicated domain account that is only allowed to link GPOs to the Test-OU.
    (T3) A GPO that is being tested MUST make this clear in the name.
    (T4) A GPO that is being tested MUST NOT be linked to a productive OU.
    (T5) GPOs that are used in production MAY be linked to the Test-OU or a Sub-OU thereof.

### (H) Handling-Rules
    (H1) Microsoft GPOs MUST remain unchanged.
    (H2) GPOs SHOULD NOT be linked to the Domain-Root.
    (H3) GPO Inheritance should be preferred to GPO Linking.
    (H4) A GPO SHALL NOT define settings for Users and Computers.
    (H5) GPO with User settings MUST be linked to a OU which MUST ONLY contain User objects.
    (H6) GPO with Computer settings MUST be linked to a OU which MUST ONLY contain Computer objects.
    (H7) GPO with User settings SHOULD only be linked to a OU that contains Computer objects if the loopback mode is enabled for these Computers.
    (H8) Permanently disabled GPOs MUST be removed.
    (H9) Permanently unlinked GPOs MUST be removed.
    (H10) Inheritance bocking SHOULD be avoided, lots of blocking could be an indication of an unfavorable OU structure.
    (H10) WMI filters SHOULD be avoided, many WMI filters could be an indication of an unfavorable OU structure.
    (H11) If GPOs are deleted, any associated security filtering groups and WMI filters MUST also be removed if they were used exclusively by the removed GPO.
    (H12) Security Filtering Groups MUST be dedicated to the usage with the GPO.
    (H13) Multiple GPOs MUST NOT share a Security Filtering Group.
    (H14) A Security Filtering Group MUST contain at least the name of the GPO and a suffix APPLY or DENY.
    (H15) If a GPO has been renamed the Security Filtering Group MUST be renamed too.
    (H16) A GPO with security settings MUST be reviewed by the owner after the review period has expired to ensure the settings are still current and effective.

### (C) Composition-Rules
    (C1) A GPO contains either a User or a Computer node, the complementary node MUST be disabled.
    (C2) Settings that serve security MUST be stored in independent GPOs and separated from other settings.
    (C3) A GPO SHALL NOT contain settings from different applications.
    (C4) A GPO for a specific application MUST have an APPKEY in its name.
    (C5) All GPOs MUST contain disjoint sets of settings.
    (C6) If a value "Disabled" or "Not Configured" has the same effect as "Enabled" with an additional value then "Not Configured" should be preferred.
    (C7) If a value "Enabled" is the same as "Not Configured" or "Disabled" is the same as "Not Configured", then this setting SHOULD only be explicitly configured if this setting is to be overridden in another GPO.

### (G) General-Rules
    (G1) All settings of all GPOs SHOULD be documented.
    (G2) All settings of all GPOs SHOULD be available as an XML report (the XML report contains the links of the GPO, which is important in the event of a restore).
    (G3) GPOs SHOULD be backed up separately from the normal system backup, e.g. via PowerShell, ideally in several versions to enable simplified recovery directly via the Group Policy Management Console.
    (G4) The metadata Tags ReviewPeriod and LastReviewDate MUST be monitored to ensure a timely review.

## Contributing
All Administrators which using GPOs in their environment are very welcome to help and make the good practices better, more useful or contribute new ideas.

## License
This project is licensed under the terms of the GPL V3 license. Please see the included Licence.txt file for more details.
