# GPO Best Practices
Collection of rules for the creation and the handling of Active Directory Group Policy Objects.

## The Rules
The best practices here are collected in six categories:

+ Names
+ Metadata
+ Test
+ Handling
+ Composition
+ General

### (N) Name-Rules
    (N1) GPOs names MUST follow a naming convention.
    (N2) Microsoft GPOs SHALL NOT be renamed.
    (N3) GPO names and descriptions must be written in English.
    (N4) The GPO SHOULD have a descriptive name.
    (N5) If a GPO makes a functional or individual setting, the name of the GPO SHOULD indicate whether something is enabled/disabled or allowed/disallowed using that GPO. In this case, the words Enabled/Disabled or Allwed/Disallowed SHOULD be used in GPO names.
    
### (M) Metadata-Rules
    (M1) Each GPO used in production MUST contain a description that adequately describes the purpose of it.
    (M2) GPOs SHOULD NOT be linked to the Domain-Root.
    (M3) 
 

### (T) Test-Rules
    (T1) Changing productive or creating new GPOs MUST follow a test procedure.
    (T2) If there is no independent test environment, GPO tests SHOULD be carried out in a special Test-OU.
    (T3) A GPO that is being tested MUST make this clear in the name.
    (T4) A GPO that is being tested MUST NOT be linked to a productive OU.
    (T5) GPOs that are used in production MAY be linked to the Test-OU or a Sub-OU thereof.

### (H) Handling-Rules
    (H1) Microsoft GPOs MUST remain unchanged.
    (H2) 

### (C) Composition-Rules

### (G) General-Rules

## Contributing
All Administrators which using GPOs in their environment are very welcome to help and make the best practices better, more useful or contribute new ideas.


## License
This project is licensed under the terms of the GPL V3 license. Please see the included Licence.txt file for more details.
