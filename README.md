# GPO Naming Standard And Best Practices
Definition of a naming standard for Active Directory Group Policy Objects.

## Motivation
The famous quote by Phil Karlton

> There are only two hard things in computer science: cache invalidation and naming things.

trifft einen teil der Realität sehr gut, vor allen dingen die sinnvolle bezeichnung von IT-Assets ist von besonderer Bedeutung macht es doch inhalte, eigenschaften, verantwortlichkeit oder abhängigkeiten leichter zu erkennen. der folgende text macht daher den versuch einen sinnvollen standard für die bezeichnung von GPOs zu entwickeln

## For Your Information.
The following text uses capitalized key words according to the Best Current Practice 14/RFC2119 (https://www.rfc-editor.org/rfc/rfc2119)

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
(1) The permitted values are literals except the items enclosed in %%, which have to be replaced through valid values. For details what is allowed inside %% please see the EBNF later in this document.

(2) Although the Application, Security Flag, Baseline Flag and Function types are all specified as optional, the standard requires that the GPO identifier MUST contain at least one of these types. For 

### **The Group Component**
One or more group entries allows grouping or sorting in the GPO Management Console. It could be grouped by status (productive or test), responsible team, location or other criteria. The grouping can also be used to control effects of various kinds, such as on backup, permissions, monitoring or inventory of the GPO.

### **The Type Component**



### **The Application Component**
In order to avoid different formulations for the same thing, so-called APPKEYs are predefined. APPKEYs encode names of applications, products, services or operating systems. The list can be expanded if necessary, but the values MUST then be used exactly as defined. The following table makes some suggestions which could be a starting point.

**The standard does not require the use of the APPKEYS specified here but rather that APPKEYS be defined and used.**


## Contributing
All Administrators which using GPOs in their environment are very welcome to help and make the best practices better, more useful or contribute new ideas.


## License
This project is licensed under the terms of the GPL V3 license. Please see the included Licence.txt file for more details.
