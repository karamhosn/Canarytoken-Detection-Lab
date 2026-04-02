# Canary Token Detection Lab

## Author
- Full Name: Karam Aboul-Hosn

## Overview
This lab examines the use of canaries for probing vulnerabilities and identifying illegitimate file access.

Under the `docs/` folder, you will find:

- `methodology.md` that describes action sequence.
- `findings.md` that consisely consolidates each section in `methodology.md`.
- `lessons-learned.md` that provides key takeaways for each section. Think of it as an extension of the `Exceptions` section below.

All lab related screenshots can be found within `methodology.md` where they are conextualized for readability. They can also be found in the `screenshots/` folder.

## Prerequisites
This lab uses Hyper-V to manage MS Windows AD DS, Pfsense, Windows 10, Ubuntu 20.04.1 VMs and uses PuTTY for SSH access. A prebuilt Docker image of a vulnerable Spring demonstration application was used for security testing. The application was launched locally in a container and exposed on port 8080 for testing purposes. The image itself was not developed as part of this project and is not included in this repository.

A description of all of the tools and their use cases in scope for this lab can be found below:

- **Canarytokens.org:** Generated DNS and PDF canary tokens
- **Hyper-V:** Managed virtual lab machines
- **Ubuntu:** Hosted the vulnerable application
- **PuTTY:** Provided SSH access to Ubuntu host
- **Docker:** Ran the vulnerable Spring/Log4j lab application
- **Burp Suite:** Intercepted and modified HTTP requests
- **Windows 10:** Tested document-based canary access

## Probing Vulnerable Services
Canaries can be used as an offensive security measure to identify vulnerabilities that are otherwise difficult to discover. When a vulnerability exists in a common library, such as Apache’s Log4J, it can be difficult to know exactly where the library is in use. This is particularly true of open-source projects that are used as components of larger projects or custom-built services. When exploit methods are known, canaries can sometimes be employed to run benign exploits against internal systems to identify vulnerable systems. In this part of the lab, we use DNS canaries to identify a system that is vulnerable to the Log4Shell exploit.  

The system that will be probed is running a vulnerable version of [Spring](https://spring.io/projects/spring-boot), a framework for developing Java applications and microservices.  

## Automating Probes
Burp suite is helpful for interactive testing, but it would be time consuming to test against many hosts and applications. Once we’ve figured out our test parameters, we can scale our testing using a scripting language like Python or PowerShell.

## Identifying Illegitimate Access
We look at using canaries to detect illegitimate file access. In this case, canaries can be thought of as miniature honeypots. These files have no legitimate use other than to lure someone into accessing them, and built-in mechanisms or external watchdog processes will alert on access. This type of canary can also be used to warn of a ransomware event. (Watchdog processes can be assigned to check for encryption of files strategically placed around the system. Should these files be encrypted, it is likely that a ransomware attack is underway.)

## Exceptions
In this lab, a file is planted that shouldn’t be accessed. When a user or malicious process poking around the network where they shouldn’t be was simulated, the token was triggered. Note that many modern applications actively prevent URL access, or they notify users prior to access. A sharp user may be able to sidestep the canary functionality because of this. Security departments should work with operational staff to ensure policies are in place that permit silent execution of canary files.  

CanaryTokens is a free service and a great learning tool. However, security organizations would be wise to run canary services in-house. This allows defenders to more precisely identify systems that accessed a file using a private IP address, and it allows for testing against systems that don’t have access to the Internet.  
