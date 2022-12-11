# Selenium Grid

There are 4 components in the Selenium suite:
1) RC - Remote Control (a.k.a. Selenium 1) -> deprecated
2) IDE - record and playback
3) WebDriver
4) Grid

__Selenium Grid__ is the 4th component of Selenium.

<img src="https://user-images.githubusercontent.com/70295997/206883687-bb9eb1af-5612-41de-8ddc-bd28d743e890.png">

 *  __DesiredCapabilites__ are used to set the type of browser and OS that I automate.
 *  __RemoteWebDriver__ is used to set the node/machine which my test runs against.
 
__Hub__
- Hub is the central point to load the tests into.
- Only one Hub per Grid.
- Hub is only launched on a single machine, eg, a computer whose OS is Windows 10 and browser is Firefox.
- Test run on the machine containing the Hub, but I can see the browsers being automated on the Node(s).

__Nodes__
 - Nodes are Selenium instances which execute the tests that I load on the Hub.
 - One or more Nodes can exist in a Grid.
 - Nodes can be launched on multiple machines with different platforms and browsers.
 - The machines running the Nodes need not match the platform of the Hub.

Download standalone Selenium and start the server. This Selenium server needs a machine. At the beginning, the Hub can be running on my Local Machine/Host with IP address 192.168.1.1:4444.
There is no external server, no Docker, no AWS - everything runs on the Local Machine. The Hub is connected to Multiple Nodes which run on the same machine.
The Test Script sends a Request to the Hub machine at the Local Host server.

The Grid is used for (1) Cross-Browser and (2) Cross-Platform testing.

Eg, in the script I pass the Desired Capabilities combination with the Chrome (browser) on a Windows machine (platform) to the server (hub). 
The Server checks for and boots an available node with Chrome on Windows. Test case TC1 gets executed on this particular (Node 1) machine.
Likewise, I have different test cases with different Desired Capabilities. These TCs get executed on different Nodes.

My entire Hub is on the Local Host machine. It's a problem! Maintenance is an issue. 
As a QE, if my laptop doesn't work or if it doesn't run 24/7, I have to move to a different level, different server/cloud/machine. 
The cloud is like a VM, eg, an EC2 instance on AWS.

I move the entire Hub machine to a different server. I request one new machine from my management. I need a physical machine next to my desk or in the server room.
And the server can be 16 GB RAM, i5 processor, or any other configs I want to have.

<img src="https://user-images.githubusercontent.com/70295997/206884114-187cc50c-fe07-470d-b4c2-c3defc6e51af.png">

This particular Hub has its own IP Address and Port Number. I have to configure the same IP : Port in my code. The code is available in my script on the Local Machine in the IDE (PyCharm, Eclipse, IntelliJ, etc). In the script I pass the the IP address and Port # of that Server that I've occupied. Then I pass the script to the Hub and the respective process happens with the Nodes (connected to the Hub).

All these Nodes can also be moved to a different machine. From my management I request 5 machines for my 4 Nodes and 1 Hub. Machine M1 is the Hub. I run it on 192.168.1.1:4444. As soon as I run the Hub Server, I can see the Grid Console/Dashboard. The Node Console is black, when no nodes are working.

<img src="https://user-images.githubusercontent.com/70295997/206884436-a981daf1-4c6c-41ca-a084-d643f83b2d18.png" width=400>




