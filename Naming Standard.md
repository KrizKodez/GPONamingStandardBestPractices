# GPO Naming Standard
Definition of a naming standard for Active Directory Group Policy Objects.

## The Rules
Each identifier of a GPO is made up of different components that MUST be separated by exactly one SEPERATOR character. The following table lists all components with their properties in the order in which they appear in the GPO identifier:

| Component | Permitted Value | Usage | Description |
| --------- | --------------- | ----- | ----------- |
| Group | %Text% | Optional | GPO grouping |
| Type | U | Mandatory | GPO with User settings |
| | C | Mandatory | GPO with Computer settings |
| | L | Optional | GPO for Loopback processing |
| | N | Optional | Settings for (N)on-Privileged User |
| | P | Optional | Settings for (P)rivileged User |
| | D | Optional | Settings for Desktop (comprise all client devices) computer |
| | S | Optional | Settings for Server Computer |
| | T0 | Optional | Settings for a User or Computer of the Tier-0 level |
| | T1 | Optional | Settings for a User or Computer of the Tier-1 level |
| | T2 | Optional | Settings for a User or Computer of the Tier-2 level |
| | F | Optional | The GPO has a filter defined |
| Application | %APPKEY% | Optional | A value of a defined list of Vendors, Applications, Operatings Systems or Services |
| Security Flag | SECURITY | Optional | Highlights that the GPO contains security settings |
| Baseline Flag | BASELINE | Optional | Highlights that the GPO contains the baseline of settings |
| Function | %Text% | Optional | Describes the settings of the GPO in a meaningful way |
| Version | %Versionnumber% | Optional | The current Version of the GPO |

### **Comments**
(1) The permitted values are literals except the items enclosed in %%, which have to be replaced through valid values. For details what is allowed inside %% please see the EBNF section below in this document.

(2) Although the Application, Security Flag, Baseline Flag and Function types are all specified as optional, the standard requires that the GPO identifier MUST contain at least one of these types.

### **The Group Component**
One or more group entries allows grouping or sorting in the GPO Management Console. It could be grouped by status (productive or test), responsible team, location or other criteria. The grouping can also be used to control effects of various kinds, such as on backup, permissions, monitoring or inventory of the GPO. In the following examples we use PROD and TEST as group definitions.

### **The Type Component**
Each GPO MUST indicate by Type whether it contains User or Computer settings. A GPO that contains User settings but is bound to an OU with only Computer objects and is used in loopback mode must display the type 'L'. Types 'U', 'C' and 'L' are mutually exclusive.

 Result | Example |
| --- | --- |
|:heavy_check_mark: Correct | PROD_U_* |
|:heavy_check_mark: Correct | PROD_C_* |
| :x: Incorrect | PROD_UC_* |
| :x: Incorrect | PROD_UL_* |

The Type 'U' could be more specified with the values 'N','P','T0','T1','T2' and the Type 'C' with the values 'D','S','T0','T1','T2'.

If the GPO uses one of the following filter types that must be indicated with the 'F' value:
+ Security Filtering Domain Group (Apply permission)
+ Delegation of Domain Group (Deny permission)
+ WMI-Filter

### **The Application Component**
In order to avoid different formulations for the same thing, so-called APPKEYs are predefined. APPKEYs encode names of vendors, applications, products, services or operating systems. The list can be expanded if necessary, but the values MUST then be used exactly as defined. The following table makes some suggestions which could be a starting point.

**The standard does not require the use of the APPKEYS specified here but rather that APPKEYS be defined and used.**

| APPKEY | Type | Represent |
| --- | --- | --- |
| ADFS | Service | Microsoft Federation Service |
| Azure | Service | Users or Computers used by Azure |
| Chrome | Application |Google Chrome Browser |
| Citrix | Product | Citrix products |
| DSM | Application | Ivanti DSM |
| Edge | Application | Edge Chromium Browser |
| File | Service | File Service |
| Firefox | Application | Mozilla Firefox Browser |
| LAPS | Application | Microsoft Local Administrator Password Solution |
| M365 | Application | Microsoft M365 |
| MDM | Application | Mobile Device Management |
| MSO2016 | Application | Microsoft Office 2016 |
| MSO2019 | Application | Microsoft Office 2019 |
| MSO2021 | Application | Microsoft Office 2021 |
| MSSQL | Service | Microsoft SQL Server |
| Notes | Application | IBM Notes |
| PKI | Service | PKI Service |
| Printing | Service | Print Service |
| W10 | OS | Microsoft Windows 10 |
| W11 | OS | Microsoft Windows 11 |
| W2012 | OS | Microsoft Windows Server 2012 |
| W2016 | OS | Microsoft Windows Server 2016 |
| W2019 | OS | Microsoft Windows Server 2019 |
| W2022 | OS | Microsoft Windows Server 2022 |
| W2025 | OS | Microsoft Windows Server 2025 |
| WSUS | Service | Microsoft Windows Update Service |
| XenApp | Application | Citrix XenApp |

If a refinement of the version is required for an application, service or operating system, this can be appended to the APPKEY in round brackets:

| Result | Example |
| --- | --- |
|:heavy_check_mark: Correct | PROD_C_W10(22H2) |
| :x: Incorrect | PROD_C_W10_22H2 |

### **The Security Flag Component**
If a GPO contains security settings, the SECURITY flag MUST be included in the identifier. It is not precisely defined here what security settings are.

### **The Baseline Flag Component**
A GPO that has the greatest possible reach or is valid for a large number of users or computers logically contains a basic configuration and MUST therefore contain the BASELINE flag. The SECURITY and BASELINE flags can be combined to indicate that the GPO contains security settings with the widest possible scope.

### **The Version Component**
The version is optional and could match the version assigned by the management console.

### **The Backus-Nauer-Form**
The following table shows the formal definition of the GPO Identifier in the EBNF form:

| Non-Terminal | Production Rule |
| --- | --- |
| LETTER | "a" \| "b" \| "c" \| "d" \| "e" \| "f" \| "g" \| "i" \| "j" \| "k" \| "l" \| "m" \| "n" \| "o" \| "p" \| "q" \| "r" \| "s" \| "t" \| "u" \| "v" \| "w" \| "x" \| "y" \| "z" |
| CAPLETTER | "A" \| "B" \| "C" \| "D" \| "E" \| "F" \|"G" \| "I" \| "J" \| "K" \| "L" \| "M" \| "N" \| "O" \| "P" \| "Q" \| "R" \| "S" \| "T" \| "U" \| "V" \| "W" \| "X" \| "Y" \| "Z" |
| DIGIT | "0" \| "1" \| "2" \| "3" \| "4" \| "5" \| "6" \| "7" \| "8" \| "9" |
| SPACE | " " |
| SEPARATOR | "_" |
| GROUP | CAPLETTER, [{CAPLETTER \| SPACE \| DIGIT}(CAPLETTER \| DIGIT)], SEPARATOR |
| TIER | "T", ("0" \| "1" \| "2") |
| TYPE | ("U", ["N" \| "P" \| TIER] \| "C", ["D" \| "S" \| TIER] \| "L"), ["F"] |
| APPKEY | CAPLETTER, {CAPLETTER | LETTER | DIGIT} |
| APPVERSION | "(" ,DIGIT, {DIGIT \| "." \| CAPLETTER}, ")" |
| APP | SEPARATOR, APPKEY, [APPVERSION]
| SECURITYFLAG | SEPARATOR, "SECURITY" |
| BASELINEFLAG | SEPARATOR, "BASELINE" |
| FUNCTION | SEPARATOR, CAPLETTER, {CAPLETTER \| LETTER \| SPACE \| DIGIT} |
| VERSION | SEPARATOR, "V", DIGIT, {DIGIT} |
| IDENTIFIER | {GROUP}, TYPE, {APP}, [SECURITYFLAG], [BASELINEFLAG], [FUNCTION], [VERSION] |

### **Examples**
+ PROD_U_W2022(22H2)_SECURITY_BASELINE

+ TEST_CT2_MSO2019_BASELINE_V10

+ PROD_CF_SECURITY_Enable Extended Protection for Authentication
   

## Contributing
All Administrators which using GPOs in their environment are very welcome to help and make the best practices better, more useful or contribute new ideas.


## License
This project is licensed under the terms of the GPL V3 license. Please see the included Licence.txt file for more details.
