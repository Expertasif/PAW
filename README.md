## How do I use this repo?

I have listed each security control in a recommended order that should be followed when starting out.  Each directory is labeled **## - Title**.  Each directory contains its own README file that details what's going on and how to apply the control. Follow the order of the numbers.  When done, work on the *xx - policy* controls in any order you desire. 

To alleviate troubleshooting, fully test your environment before continuing on to the next section.  Literally spend several days living under the new policy to see how things work. 

Where a script is concerned, specific instruction and requirements to run the script can be found within the script's comment header.

## Privileged Access Workstation (PAW)

**What is a PAW?**

In short, a PAW is one solution to the problem of credential theft, replay and pivoting attacks, and privilege escalation.  PAW is a method of administrating network devices in a more secure and more hardened environment than what most admins are used to.  A successful PAW deployment will contain many security controls aimed to enable a more [Defense in Depth](https://en.wikipedia.org/wiki/Defense_in_depth_(computing)) security strategy.

**Okay, but what is a PAW?**

A PAW is the workstation the admin uses to access and administrate the network using privileged credentials.  It provides the admin a secure method to perform day-to-day administrative tasks on network devices such as Domain Controllers, member servers, user workstations, networking equipment, and cloud admin portals (like Azure and AWS).  Because the PAW adheres to the [Clean Source Security Principal](https://docs.microsoft.com/en-us/windows-server/identity/securing-privileged-access/securing-privileged-access-reference-material#CSP_BM) it prevents the logged on user from freely surfing the Internet, checking email, running applications outside of the AppLocker whitelist, or insecurely accessing network devices that could expose risk to credential theft.  It provides the admin everything they need to do their job and nothing more [Least Privilege Security](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

**How is a PAW physically different than a normal workstation where I administrate my servers with RDP and MMC?**

The PAW is a physical workstation, preferably a laptop, that runs Windows 10 Enterprise Edition (1709+) as the primary host OS.  This device is used to administrate the network and all the systems on it.  It has the Hyper-V role installed that, in addition to security features like Credential Guard, hosts a VM that provides the admin day-to-day Internet access and email.  PAWs have several hardware requirements to make for the most secure deployment:

- Windows 10 compatible (no Chrome books or Mac)
- TPM 2.0
- Enough hard drive, CPU, and RAM resources to have a pleasant experience in your day-to-day VM

Consider buying from a vendor that has frequent firmware updates and a long support life-cycle.  Specialized hardware like Sony Vaio and Alienware should also not be considered.

Additionally, you should be aware of DMA attacks and consider purchasing hardware that does not come with DMA ports (Thunderbolt, PCI-E, Firewire, ExpressCard).  See [Sami Laiho's Win-Fu Blog](http://blog.win-fu.com/2017/02/the-true-story-of-windows-10-and-dma.html) for more details about DMA attacks and mitigation.

If a single workstation that handles the load of two is not optimal for your environment, you can split the roles onto separate laptops.  One workstation for secure administration, and one for Internet and email.  

**Is it difficult to configure PAWs?**

The main purpose of this repo is provide baseline configuration templates and walkthroughs to make the configuration simpler.  Initially, it is quite complex.  As I look at my GPOs that are designed to address only PAWs, I count 36 and growing.  The biggest complexity, however, is changing your IT team's behavior around remote administration.  You will be doing things very different than you are used to.  I like the saying, *it is fundamentally impossible to improve something wilst keeping it the same*.
