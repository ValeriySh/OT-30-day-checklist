# OT Critical Infrastructure: 30-Day Checklist

The checklist is the Excel workbook in this repository: [**OT Critical Infrastructure 30-Day Checklist.xlsx**](https://github.com/ValeriySh/OT-30-day-checklist/raw/refs/heads/main/OT%20Critical%20Infrastructure%2030-Day%20Checklist.xlsx).

## What this is?

A list of technical actions that a critical infrastructure organisation can complete in 30 days with its own staff, written for a near-emergency (which is where we are right now). Every row says what to do, how to do it with minimal tooling, how much effort it takes, what "good" looks like, what to do if you find a problem, and what evidence to keep.

## Who is this for?

For people who run networks, control systems and IT at critical infrastructure organisations: energy, water and wastewater, transport, manufacturing, chemicals, food, health, and any other organisation that runs a control system.

The checklist assumes limited security tools and, by default, no dedicated OT security staff: the rows tagged Small are written for a team of 1 or 2 people who also run the network or the plant. The rows tagged Medium and Large add what a larger team, or one with dedicated OT security staff, should do in the same 30 days (see Team size). Security specialists will find the technical detail in the tab Commands and in the reference columns at the right of the Checklist.

## Why now?

1. In late July 2026, attackers reached more than 30 community water systems in Minnesota in one weekend. Utilities in at least 12 US states then reported similar incidents. CISA later counted more than 100 internet-exposed systems targeted in the water and wastewater sector in July alone, most of them PLCs connected directly to a cellular modem. The attackers changed passwords and IP addresses, locked operators out, and caused loss of monitoring and control. Some utilities went to manual operation and issued boil-water notices. CISA said that utilities of all sizes were targeted, including some with mature security programs, and told operators to remove exposed PLCs from the internet and to keep a known clean backup of every PLC image. No formal attribution has been made; media reporting points to Iran-linked actors.

2. In December 2025, a state-sponsored campaign deployed wipers at more than 30 wind and solar sites and a combined heat and power plant in Poland. The attackers entered through exposed firewalls without MFA, held access at one plant for about 9 months, and delivered the wipers through Active Directory Group Policy. Endpoint protection stopped the wipers at some sites.

3. In 2026, firewalls and VPN gateways were the main way in. In January, attackers created administrator accounts on fully patched devices of one major vendor. In June, credentials from about half of that vendor's internet-facing firewalls were exposed, and CISA ordered session termination, credential rotation, MFA and removal of management interfaces from the internet. In July, a patch bypass for a persistence technique was added to the KEV catalogue. Patching alone does not evict an intruder.

4. Russia's war against Ukraine is escalating again, and the hybrid activity around it is growing. In late August 2026, NATO said that Russia is intensifying its attacks on Ukraine and expanding its hybrid activity across Europe. In May 2026, the head of GCHQ said that Russia is scaling up its daily hybrid activity against the UK and Europe and is targeting critical infrastructure. Canada's National Cyber Threat Assessment 2025-2026 judges that state actors are very likely pre-positioning in critical infrastructure networks in Canada and allied countries for possible future disruptive or destructive operations.

5. On the night of October 11 to 12, 2026, attackers took remote control of the refrigeration controllers in hundreds of supermarkets in France and ran the freezers and cold rooms at up to 50 degrees Celsius for about 6 hours. Food had to be thrown out, fires were reported, and Intermarche put the loss at tens of millions of euros in a single day. The controllers were Danfoss refrigeration management units with a web interface reachable from the internet so that the maintenance companies could adjust them remotely; Danfoss said the affected units ran outdated firmware. In August 2026, Claroty had published a login bypass and a remote code execution flaw for the same controller family (CVE-2025-41450, CVE-2025-41451; fixed in firmware R4.3.1) and had counted 2,765 of them exposed to the internet. On the same day, Ahold Delhaize (Albert Heijn in the Netherlands, Delhaize in Belgium) took systems offline for a security incident of its own; it said it saw no link to the French attacks.

## Guiding principle

Assume that IT is compromised, but it must not affect the OT. IT is attacked every day, and the corporate Active Directory will fall at some point.

For every path, system and change, ask one question: could a compromise of IT reach OT through this? If the answer is yes, the row that closes it comes first.

This leads to a small number of rules: no shared Active Directory; management tools and interfaces for OT live on the OT network; virtualisation, switching, firewalls, routers and wireless that serve OT are dedicated to OT and managed from OT; the OT backup system is not reachable from IT; the safety systems are reachable from nothing but their own engineering station. The same technology on both sides is fine; sharing an instance is not. What cannot be separated in 30 days goes on the roadmap [Hold H-10] with a date.

## Team size

Some critical infrastructure sites are defended by 1 or 2 people who also run the network or the plant. The column Team in the Checklist and on Start here marks the smallest team that should do each row, in the way the CIS Controls use implementation groups, but for the defending team rather than the organisation:

- Small: 1 or 2 people. The rows marked Small are the minimum set. The full Small set is about 50 person-days of work, which 2 people who also run a plant do not have in 30 days; so for Small teams the deadline in By when applies to the column Minimum today (the 1-hour version of the row), and the full row is due by Day 30. Rows with no Minimum today are short enough to do in full.
- Medium: 3 to 6 people, or a small team with an IT department that helps. Adds the deeper reviews and the watch on DNS, hosts and new devices. Deadlines apply to the full row.
- Large: a team with dedicated OT security staff. Adds the passive sensor, the historian log review and the dedication of shared infrastructure.

The tags are cumulative: a Medium team does the Small and Medium rows; a Large team does all rows. Small cells are shaded green. The tag says who should do the row; the deadline says when the decision and the request must be made, and management of change says when the change happens (see Safety rules).

## How to use it

1. Read the tab Start here. It is the order through the Checklist: 18 steps over 30 days, each pointing at the rows that do the work. It is an overview; tick rows in the Checklist, not on Start here.
2. Work the tab Checklist from the top. It holds every row, sorted by the column By when and then by the Start here step, so the top of the list is Start here expanded. Filter on Phase (Detect, Find, Stop, Check, Hold), on Team, or on Who does it with the text filter Contains and your role, to work one part of the list. A team of 1 or 2 people filters on Team = Small first.
3. Detect rows come first and most take hours, not days; they capture the baseline and start looking for intruders who are already inside. Rows marked then daily or then weekly keep running after Day 30. The passive sensor [Detect D-03] comes after the first cuts, not before.
4. Stop rows reduce the attack surface. Row [Stop S-16] (isolate the safety systems) is due by Day 3. Row [Stop S-05] (brokered vendor access) comes before row [Stop S-06] (remove direct vendor access).
5. Check rows look for intruders who are already inside and run in parallel with the Stop rows. Row [Check C-12] is the exit into incident response; read it on Day 1.
6. Hold rows, from Day 21, verify that the changes held, test the islanding procedure and make Detect permanent.
7. Fill the columns Status, Owner and Date done. Use the tab Change Register for every Stop change and every exception; use the tab Detect Log every day.
8. The column Tools lists free or built-in tools; use these or similar tools if you already have them. A commercial tool that does the same job is fine. The tab Commands gives command lines for those tools, keyed by row ID; the Checklist links to them. Every address, name and path in them is a placeholder. The commands were written from documentation and memory, not run in a lab: validate each one on a test device or in a maintenance window before running it in production, and treat the FortiOS and Cisco IOS lines as examples of the shape of the change for one product and version.
9. Deadlines are for the decision and the request. Any change that touches a production path (a firewall rule, a safety system, a controller credential) goes through your management of change, and the Change Register is that record. The Minimum today column gives the part of each heavy row that needs no MOC or can be done inside a normal window.

## Safety rules

1. Never run an active scanner (Nmap, vulnerability scanner) inside OT networks as many controllers stop working when they are scanned. Scan only your own public ranges from outside with written permission.
2. Coordinate every change with operations; use an agreed window and have a rollback path written down before you start.
3. Give vendors and integrators the brokered path [Stop S-05] before you remove their direct path [Stop S-06]. A plant without vendor support will revert your change within a week.
4. Export the configuration and the logs before you change, update or reboot a device.
5. Do not clean, reboot or re-flash a device that may be compromised before you have read the vendor guidance and preserved the evidence. Some persistence survives updates; some evidence does not survive a reboot.
6. When you isolate a suspicious host, isolate it from the internet and from IT. Isolate it from the process only when operations agree.
7. Any work on a controller takes 2 people; observe first and change later, with a work order. During checks use the vendor upload (read) functions only; never write to a controller.
8. Rotate credentials first, then update, then verify. Treat every credential that lived on an exposed device as known to the attacker.
9. Network sensors are passive only: a SPAN or mirror port or a TAP, never inline. Confirm that the sensor cannot transmit.
10. Read-only host tools first, and nothing installed on an HMI or SCADA server without a vendor statement: the baseline snapshot and the host reviews run from removable media or a share and leave nothing behind. Do not run memory-heavy tools on old hosts during production without operations.
11. Hazardous areas: in a classified area (Zone 0, 1 or 2; Class I Division 1 or 2) a phone or a laptop is an ignition source. The walk-downs and the wireless survey happen from unclassified areas or with intrinsically safe devices; the site's hazardous-area map governs.
12. Management of change is not suspended by this checklist. Deadlines say when to decide and request; the site's MOC says when the change happens. The rows that need no MOC say so.

## If you find signs of compromise

Follow row [Check C-12]: stop, preserve, isolate, report. Write the phone numbers here before Day 1:

- National cyber centre (Canada: Canadian Centre for Cyber Security, cyber.gc.ca; United States: CISA, cisa.gov): \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
- Incident response provider: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
- Sector ISAC or association: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
- Decision maker who can order the OT disconnect [Stop S-13]: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

## Get ready before Day 0

Free or built-in tools that the rows use. Use these or similar tools if you already have them; a commercial product that does the same job is fine.

- External exposure: Shodan (shodan.io) and Censys (search.censys.io) to see what the internet sees; Nmap (nmap.org) to scan your own ranges from outside; the CISA KEV catalogue (cisa.gov/known-exploited-vulnerabilities-catalog) to check edge device versions.
- Network sensor: CISA Malcolm (cisa.gov/resources-tools/services/malcolm) or Security Onion (securityonionsolutions.com); both run Zeek and Suricata, and Malcolm parses OT protocols. RITA (github.com/activecm/rita) finds beacons in Zeek logs. Eligible small utilities (US or Canada; water, electric or natural gas; under 100 million USD revenue) can apply to the Dragos Community Defense Program (dragos.com/community/community-defense-program) for the Dragos Platform and Neighborhood Keeper at no cost.
- Log collector: rsyslog or syslog-ng on a Linux VM; CISA Logging Made Easy (cisa.gov/resources-tools/services/logging-made-easy) for Windows networks with Active Directory; Wazuh (wazuh.com) for Windows and Linux agents and file integrity monitoring.
- Host snapshot: Microsoft Sysinternals (learn.microsoft.com/sysinternals) for Autoruns, Sigcheck, Process Explorer and TCPView on Windows; auditd and the built-in ps, ss, systemctl and crontab on Linux; Velociraptor (docs.velociraptor.app) or osquery (osquery.io) to collect from many Windows and Linux hosts at once.
- Active Directory review: PingCastle (pingcastle.com) and Purple Knight (purple-knight.com).
- Event log triage: Hayabusa (github.com/Yamato-Security/hayabusa) for fast Windows event log review.
- Brokered access: Windows Remote Desktop Gateway with an MFA provider, or Apache Guacamole (guacamole.apache.org).
- Media control and file integrity on Linux: USBGuard (usbguard.github.io) and AIDE (aide.github.io).
- Mapping: MITRE ATT&CK Navigator (mitre-attack.github.io/attack-navigator) with the ICS matrix, to track which techniques your rows cover.

## Column guide

- ID: row reference; the letter is the phase (D Detect, F Find, S Stop, C Check, H Hold), and references use the form [Phase ID], for example [Detect D-04].
- Phase: the kind of work; Find and Stop reduce the attack surface, Detect and Check find intruders and changes, Hold verifies and makes things permanent.
- By when: the day the row must be done by, counted from Day 0; then daily, then weekly or then monthly marks a row that repeats.
- Start here step: the step on the tab Start here that uses this row.
- Team: the smallest team that should do the row (Small, Medium, Large; cumulative; see Team size). Minimum today: the 1-hour version of a heavy row, which needs no MOC or fits a normal window; Small teams do it by the deadline and the full row by Day 30.
- Effort: hours, a day, days, or a week or more, for one person who knows the environment.
- Who does it: the role, not a person. The lead role comes first; with names who joins; or means either role can do it. OT means the OT, controls or instrumentation team; Systems means the Windows and Linux server and workstation administrators; AD means the Active Directory administrator. To see every row that names your role, use the text filter Contains on this column.
- Check: what to do.
- How: steps with minimal tooling.
- Good looks like: the pass criterion.
- If you find a problem: what to do next.
- Evidence to keep: what you keep for the Change Register and for a later audit.
- Tools: free or built-in options; use similar tools if you have them.
- Commands: a link to the tab Commands, which holds command lines for the tools named in the row, one per line, with addresses, names and paths to replace; vendor lines are examples for one product and version; validate before running.
- Status, Owner, Date done, Notes: fill these in.
- The last 7 columns are reference only and can be collapsed. The mapping shows which adversary behaviours a row touches, not that the row stops or detects them; do not count mapped techniques as covered techniques. Asset types: MITRE ATT&CK for ICS asset names.
- ATT&CK technique, mitigation, detection strategy: MITRE ATT&CK for ICS v19.2 identifiers; names are in the tab MITRE Reference.
- IEC 62443-3-3 SR: the system requirement the row supports.
- CSF 2.0 function: NIST Cybersecurity Framework 2.0 function.
- SANS ICS critical control: which of the SANS ICS Five Critical Controls the row serves (1 incident response plan, 2 defensible architecture, 3 network visibility and monitoring, 4 secure remote access, 5 risk-based vulnerability management).

## Scope

This document covers OT and the IT that reaches it: internet-facing edge devices, remote access, Active Directory and Group Policy, jump hosts, and the servers and workstations that manage control systems. Entities where IT is the service (air carriers, financial services, digital providers) are out of scope; see the note on IT systems below. Airport operators and air navigation providers are in scope.

Sectors where OT is the service (energy, water and wastewater, pipelines, chemicals, manufacturing, rail, ports, airports and air navigation) use the whole list. Sectors where OT only supports the service (building management, medical devices, laboratory and data centre facilities) use the Find, Detect and Hold rows and apply [Stop S-01], [Stop S-05] and [Stop S-07] to those systems. Managed service providers and integrators apply the brokered access rows [Stop S-05] and [Stop S-06] to their own access into client OT.

Host rows apply to any operating system; the How column gives Windows and Linux steps side by side. Appliances on embedded Linux or an RTOS (HMI panels, gateways, protocol converters, controllers) are handled as devices: credentials in [Stop S-07], configuration and firmware in [Check C-06].

## IT systems

There is no 30-day version of this list for the wider IT estate (email, user workstations, business applications, cloud services). The attack surface is many times larger than OT, and the basics that protect it (endpoint protection everywhere, tested backups, patching and vulnerability management, MFA on every account, least privilege) take months to implement well. OT is different: it is usually isolated already, and it needs a short list of hard cuts and a watch, which is what this document is.

The IT that reaches OT is inside this list, because most OT incidents start there: the July 2026 water attacks came through cellular-connected controllers, the December 2025 Poland attacks through exposed firewalls and Group Policy. Do those rows first.

For the rest of IT, adopt an existing baseline after Day 30 rather than waiting for another checklist: CIS Controls v8.1 Implementation Group 1 (essential cyber hygiene), the Cyber Centre's Baseline Cyber Security Controls for Small and Medium Organizations, or the CISA Cross-Sector Cybersecurity Performance Goals 2.0. Pick one and work through it. During the 30 days, one IT rule matters for OT: nothing new crosses the IT/OT boundary without an entry in the Change Register.

## References

- MITRE ATT&CK for ICS v19.2: https://attack.mitre.org/matrices/ics/
- MITRE ATT&CK campaign C0063, 2025 Poland Wiper Attacks: https://attack.mitre.org/campaigns/C0063
- CISA, FBI, EPA, DOE, Primary Mitigations to Reduce Cyber Threats to Operational Technology (May 2025): https://www.cisa.gov/resources-tools/resources/primary-mitigations-reduce-cyber-threats-operational-technology
- CISA advisory AA25-343A, Pro-Russia Hacktivists Conduct Opportunistic Attacks Against US and Global Critical Infrastructure (December 2025): https://www.cisa.gov/news-events/cybersecurity-advisories/aa25-343a
- CISA advisory AA26-097A, Iranian-Affiliated Cyber Actors Exploit Programmable Logic Controllers Across US Critical Infrastructure (April 2026, updated July 2026): https://www.cisa.gov/news-events/cybersecurity-advisories/aa26-097a
- CISA alert, CISA Urges Water and Wastewater Systems Sector to Protect OT Against Activity Targeting PLCs (July 30, 2026), and CISA exposure reduction guidance for internet-exposed OT (August 21, 2026): cisa.gov
- FBI and EPA public service announcement I-073026-PSA, Malicious Cyber Actors Targeting Water and Wastewater Sector Internet Facing Programmable Logic Controllers (July 30, 2026): ic3.gov
- Canadian Centre for Cyber Security, National Cyber Threat Assessment 2025-2026 (October 2024), and the Cyber Centre threat bulletins on Russian-backed cyber threat activity against Canadian critical infrastructure: cyber.gc.ca
- Congressional Research Service, Russian Hybrid Warfare Activities in Europe (R49134, August 2026): https://www.congress.gov/crs-product/R49134
- CISA and partners, Foundations for OT Cybersecurity: Asset Inventory Guidance for Owners and Operators (August 2025): https://www.cisa.gov/resources-tools/resources/foundations-ot-cybersecurity-asset-inventory-guidance-owners-and-operators
- CISA, Cross-Sector Cybersecurity Performance Goals 2.0 (December 2025): https://www.cisa.gov/news-events/alerts/2025/12/11/cybersecurity-performance-goals-20-critical-infrastructure
- CISA, Known Exploited Vulnerabilities catalogue: https://www.cisa.gov/known-exploited-vulnerabilities-catalog
- CISA alert on Fortinet authentication bypass CVE-2026-24858 (January 2026): https://www.cisa.gov/news-events/alerts/2026/01/28/fortinet-releases-guidance-address-ongoing-exploitation-authentication-bypass-vulnerability-cve-2026
- CISA Malcolm: https://www.cisa.gov/resources-tools/services/malcolm
- CISA Logging Made Easy: https://www.cisa.gov/resources-tools/services/logging-made-easy
- CISA critical infrastructure sectors: https://www.cisa.gov/topics/critical-infrastructure-security-and-resilience/critical-infrastructure-sectors
- Canadian Centre for Cyber Security, Cyber Security Readiness Goals (October 2024): https://www.cyber.gc.ca/en/cyber-security-readiness
- Canadian Centre for Cyber Security, Baseline Cyber Security Controls for Small and Medium Organizations: https://www.cyber.gc.ca/en/guidance/baseline-cyber-security-controls-small-and-medium-organizations
- CIS Critical Security Controls v8.1, Implementation Group 1: https://www.cisecurity.org/controls
- Directive (EU) 2022/2555 (NIS2), Annex I and Annex II sectors.
- IEC 62443-3-3, System security requirements and security levels.
- IEC 61511-1:2016, Functional safety, safety instrumented systems for the process industry sector, clause 8.2.4 (security risk assessment).
- SANS, The Five ICS Cybersecurity Critical Controls (2022): https://www.sans.org/white-papers/five-ics-cybersecurity-critical-controls/
- Dragos Community Defense Program: https://www.dragos.com/community/community-defense-program

## Authors

Val Shevtsov (https://www.linkedin.com/in/valshevtsov/)

## Licence

CC BY-SA 4.0. https://creativecommons.org/licenses/by-sa/4.0/
