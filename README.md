# Testing-EDR-Effectiveness
This Repository describes the methods with which you can test out your EDRs efficiency.

Describes the overall test case design, implementation, and 
execution of the EDR Tool efficiency analysis.

Objectives: The main objective of this analysis is to identify the potential gaps in an EDR tool and 
to mitigate them.

We have divided the analysis into 4 main sections
1. Events captured by the EDR tool: What are the various logging events that are captured by 
the sensor( Windows, Linux, MacBook, Containers) they include items like below:\
    Command line activities\
    Logon, logoff activities\
    File access and modifications\
    DNS Network and port events\
    Registry changes\
    File downloads

2. Known malicious files:
    a. Download set of known malicious files and identify which amongst them were correctly identified and blocked by the hashes
    b. Download filess malware(lolbas,python,js) and execute them and observe the telemetry and see if the EDR tool correctly idetifies the malware or uses the IOA.
   
3. Red Team Emulation: Identify various TTP mapped on to MITTRE that are correctly identified 
and prevented by the EDR tool.

Procedure:
1. We will require 1 C2 server where we will be hosting MITTRE Caldera.
2. We will have Windows, Linux, containers, and MacBook with EDR Tool.
3. Using Caldera emulation tool, a TCP reverse proxy will be setup from the individual hosts.
4. We will run MITTRE TTP using atomic tests on these individual servers via C2.
5. Individual tests for the various event types will be conducted locally on each server and will 
be observed via events portal on the EDR tool.
6. Samples of malware will be obtained via Malwarebazaar: bazaar.abuse.ch and loaded on to 
test server and EDR Tool findings will be observed.

4. Threat Intel Integration
   How well does the EDR tool integrate with their own threat intel solution and how rich is the context
   a. We will take 15 sample IOA with a combination of malicious IP adress, dns of TOR exit nodes, known C2 servers etc and do both a curl and a dns query to them from the analysis machine
   b. Observe how well the EDR tool correctly identifies the malicious indicators
   


Known malicious files:
This test is to identify the efficiency of EDR Tool to identify known malicious files by only their 
hashes.
Procedure:
1. We downloaded 15 malware samples with multiple hits on virustotal onto a test server and unzipped the folder.
2. Identify if the file was auto quarantined by the EDR and wait for an alert for the same.

Filess malware:
This test is to identify the efficiency of EDR Tool to identify malware during the execution phase when the indicators will be loaded into memory
Procedure:
1. We downloaded 5 malware samples based on different use cases like ransomware, coinmining etc which soleley run in memory or have an initialization script written in python, js and loads into memory.
2. Identify if the malware when executed triggers anything on the edr in relation to the suspicious activity, the IOA,IOC


Red Team Emulation Tests:
The below set of tests was to emulate an entire chain of events from initial access, execution all the 
way to impact testing out the various tactics and techniques in the MITTRE framework and 
determine what all are correctly identified by EDR Tool and prevented and what all are not.
Test Case Identify Agent Communication to C2:
1. The first set of tests involve the correct identification of a malware which will be used to 
connect back to the C2 server.
2. This was conducted in two different ways 
a. Pre EDR Tool installation: To identify if the malware sample or beaconing activity 
is correctly identified once EDR Tool is installed at a later stage.
b. Post EDR Tool: To identify if the malware sample or beaconing activity is correctly 
identified by EDR Tool during initial payload drop.

The red team emulation tests were conducted with MITRE Caldera: a red team emulation tool designed with atomic test cases built into it.
https://caldera.mitre.org/#:~:text=A%20Scalable%2C%20Automated%20Adversary%20Emulation,energy%20through%20automated%20security%20assessments.

https://github.com/mitre/caldera

https://www.mitre.org/our-impact/intellectual-property/caldera

The Emulation campaigns for windows and linux are in the yaml files.
