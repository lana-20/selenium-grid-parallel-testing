# Parallel Testing

_Parallel Testing_ is essential in web UI test automation. It decreases the execution time and costs dramatically. From the Agile testing perspective, it allows for fast deploy-and-ship plus frugality with the budget and human capital.

<img width="800" alt="image" src="https://user-images.githubusercontent.com/70295997/213115529-5029e2f1-0286-4afd-8f04-7dbad2bdc365.png">

To see how parallel testing can enhance regular automation testing, consider a basic example of an automated functional test for a sign-up form. If we were to run this test on 45 different browser and operating system configurations, with each test taking an average of 2 minutes, then the total test time would be 90 minutes or 1.5 hours if run in sequence.

If I were to run 3 parallel tests simultaneously, the total execution time would be reduced to 30 minutes. And if we were to run 6 parallel tests, the total execution time would be further reduced to 15 minutes, which is a significant decrease compared to running them in sequence.

![image](https://user-images.githubusercontent.com/70295997/213121653-d8164365-80eb-419f-b41b-c20ddc09745f.png)![image](https://user-images.githubusercontent.com/70295997/213121718-03532f7f-f3a2-414a-9be2-33ee7ffd7916.png)


As more software engineering teams adopt the CI/CD model, the pressure to quickly release high-quality products is growing. In quality assurance (QA), one way to minimize the impact of bugs is to test code early and fail quickly. To achieve this, QA teams need to increase [test coverage](https://github.com/lana-20/test-coverage) through automation. However, the large number of tests that need to be performed and the limited time available for testing can make it difficult to rely solely on sequential automated tests. Parallel testing enables teams to simultaneously run automated tests across multiple configurations, which helps to address constraints related to time and budget while also increasing test coverage and improving quality.

Parallel Testing is a technique that utilizes automation testing by allowing the same tests to be run at the same time in different environments, on various device and browser configurations. The primary aim of parallel testing is to minimize time and resource limitations. Unlike distributed testing, where different testing components interact with each other, parallel testing does not involve any interactions between test components.

_Parallel Execution_ can be achieved by using Selenium Grid, CI/CD tools like Jenkins, remote driver connection (set up via the DesiredCapabilities JSON object in the test script) to a cloud service like AWS or cloud-based test lab like BlazeMeter, LambdaTest, or SauceLabs, and container orchestration service like Docker. Running tests in parallel can significantly reduce the time needed to complete even the most tedious test suites.

![image](https://user-images.githubusercontent.com/70295997/213120888-91ab5c62-40ab-4286-abe3-d38513b2b5e7.png)

_Parallel Execution_ can be achieved by using Selenium Grid, CI/CD tools like Jenkins, remote driver connection (set up via the DesiredCapabilities JSON object in the test script) to a cloud service like AWS or cloud-based test lab like BlazeMeter, LambdaTest, or SauceLabs, and container orchestration service like Docker. Running tests in parallel can significantly reduce the time needed to complete even the most tedious test suites.

# Selenium Grid

There are 4 components in the Selenium suite:
1) RC - Remote Control (a.k.a. Selenium 1) -> deprecated
2) IDE - record and playback
3) WebDriver
4) Grid

__Selenium Grid__ is the 4th component of Selenium.

<img src="https://user-images.githubusercontent.com/70295997/206888643-964d0057-bec1-452d-b430-c5adaabf35e2.png">

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

All these Nodes can also be moved to a different machine. From my management I request 5 machines for my 4 Nodes and 1 Hub. Machine M1 is the Hub. I run it on 192.168.1.1:4444. As soon as I run the Hub Server, I can see the Grid Console/Dashboard. The Node Console is black, when no nodes are working. Register Nodes with the Hub to establish connection.

<img src="https://user-images.githubusercontent.com/70295997/206889723-607550f1-c4b8-41d1-bc79-e075877749f8.png" width=600>
<img src="https://user-images.githubusercontent.com/70295997/206889952-a30f30bd-caab-42e8-8d44-15f7ef591a87.png" width=400>

I can move this entire configuration to a different machine that is also a Local Machine. On the Local Host, my code contains Desired Capabilities, Host IP address, browsers and platforms I want to run. Based on that script, I send a request to the Hub to get executed on the Nodes.

The entire infrastructure must be on the same Network. On my Local Host, the Hub IP must be white-listed, which is attainable when on the same network. Test case scripts run on respective node machines.

<img src="https://user-images.githubusercontent.com/70295997/206888794-572b00fc-b429-481c-bc7f-e0c90a8f65ab.png">

### Setup Selenium Grid

1. Local
2. Different machines/servers (Local)
3. Set in the form of Docker
4. Cloud (AWS, Azure, GCP, etc.) - install Docker container. Example: Set up Selenium Grid on AWS Docker container.
5. Remote Labs (Saucelabs, Browserstack, Lambdatest)

For Safari there's no container, only for Chrome and Firefox. Apple does not provide any container for Safari Driver.

<img src="https://user-images.githubusercontent.com/70295997/206892243-21f32232-fc88-455a-8f57-1fa641c1553d.png" width=400>


Can host the Grid on Local, any other server, AWS cloud, or remote test labs. Just need the Hub Server IP address to set up on any machine. Configure it (the IP) in my Local (DesiredCapabilities), push the code to _master_ and trigger it.

![image](https://user-images.githubusercontent.com/70295997/206893820-fe6d3ba8-6646-497d-b6e8-946755ecf139.png)


Do not maintain the Master Branch inside the Hub. But how to generate reports? Reports always generate in my Local, because of the build path (project folder path).

If running in Jenkins, Reports are generated in Jenkins under the Build Number:
- Allure
- Html Reports
- Extent

Eg, in Jenkins go to Build # 101, report it, and locate the Allure report in that particular Build.
<img src="https://user-images.githubusercontent.com/70295997/206930532-93831b7e-66e9-4a4e-968d-fc2cfb61981d.png" width=800>

Use Remote WebDriver (RWD) with Desired Capabilities (DC).
Set up an EC2 machine on AWS.

![image](https://user-images.githubusercontent.com/70295997/206938058-d2ab36a3-1ce2-4ebd-a2c8-212428f5201e.png)

Through my Docker Container, I create a Hub (C1) and its own IP address, on an AWS EC2 instance. On the same machine, I can create multiple Nodes, in the form of Containers:

- Node 1 - Container 2 - C2
- Node 2 - Container 3 - C3
- Node 3 - Container 4 - C4
- ...

On a node container, with the help of Selenium, I have Chrome of Firefox installed. No Safari containers. 

When I install this infrastructure through Docker [container], the Hub is connected to all the Node containers. I can maintain all 7 containers (1 Hub + 6 Nodes) on the same EC2 machine. Or, I can take a cluster of 6 EC2 instances and connect the Hub to it. However, this may incur unnecessary costs for EC2 instances. It's better to create 1 EC2 on AWS and configure all the Grid setup there.

The whole concept remains the same. On the same machine, I have the Hub set up on IP Address 201.9.10.11 : Port Number 4444. All the Nodes have their own IP Address and Port Number. All these are Linux Machines. 95% of the containers available on the market are Linux containers. I'm uncertain if Windows containers are availalble for Selenium Chrome, Firefox or other browsers. Most of the containers I work with are Linux machines. Each Linux machine has its own IP and Port, the same IP:Port as in the Hub Server. All the Nodes and the Hub are connected through Docker Containers and are available on my AWS machine.

I have my code with Desired Capabilities, which contains the IP address and Port number matching those of the Hub IP:Port.
<img src="https://user-images.githubusercontent.com/70295997/206939796-5b520641-5289-490f-a5ab-e50cc2bc3435.png" width=600>

And I push this code to the Master Branch. Same way, I can pull the Master's latest code to my Local, if I want to run the code on a particular cloud.

I create a Jenkins Server, configure a Job or a Pipeline in it. Inside the Job, I provide the path to my particular Git repo. From it, I trigger a Job. Then my code gets compiled and executed. My test gets executed from there. In this part, the test checks if this particular Master Repo has these particular Desired Capabilities, when I launch my WebDriver.

<img src="https://user-images.githubusercontent.com/70295997/206964372-c5392bea-2e23-4c15-b146-8bd74ce9501a.png" width=800>

I launch my WebDriver with Remote WebDriver (RWD) from my Local. On my Local, I've already configured that I have to use RWD to run tests on the Hub machine (WebDriver driver = RWD).

RWD is responsible for executing tests on a remote machine. A remote machine can be anyrhing - on AWS EC2 instance, on my Docker, on Saucelabs, etc. In my case, it's an AWS EC2 instance.

I pass the Hub IP:Port configuration to RWD. In the same code that I have on my Local. I push that code to the Master Repo and trigger the Jenkins Job. Through Jenkins I trigger my test cases on the AWS EC2 instance. IP address white-listing is configured there - on AWS I have to provide the IP address for inbound loads. It means that any Requests coming from this specific Jenkins server get accepted and not blocked.

The Jenkins Request is sent to the Hub Server. The Hub recognizes a Chrome machine and executes on Container 1 (C1). It means that if I pass 10 test cases and give a thread count of 5 (through my TestNG, or xml, etc.) it executes in Parallel mode. First, it passes through the 4 availalble Chrome containers, then make another pass through 1 Chrome container. Same with Firefox.

In Parallel mode I can execute Cross-Browser and Cross-Platform testing. In this case, Cross-Platform testing is not feasible, because I have no Windows available. An instance is available, but the container is not. If I really have to, I can create a Windows node with Firefox and Chrome.

If I don't want to maintain Jenkins, then my Local runs on TestNG. TestNG executes my code on the specific Hub Server machine (on AWS cloud) from Local. Because I've configured the same Hub IP:Port in my Local script.

What if I want to execute on my Local? I don't want a bunch of web browsers on AWS. I just have to put a condition/flag in the script.

    # Local

    if RemoteFlag = True:
     RWD(IP:Port)
    else:
     Local -> WD driver = new ChromeDriver()

If RemoteFlag is False, it executes on Local machine.
If RemoteFlag is True, it means I'm trying to run on remote driver. It should execute on the container, i.e. Selenium Grid side on the particular container or AWS machine.

<img src="https://user-images.githubusercontent.com/70295997/206972260-abd47dc8-8794-44f0-bec4-802ef40c36d9.png" width=600>

Do not store the Master Branch on the Hub. It means I'd have to store/maintain a Jenkins machine inside the Hub -> Bad practice!

Instead store the Hub and Nodes on their own separate (virtual) machines with their own respective IP addresses. Retrieve the Reports from either Local or Jenkins job build number.
![image](https://user-images.githubusercontent.com/70295997/206976013-2a2f1dae-30ed-4ec4-afd4-8d0a2ad75e2c.png)

____

[Parallel Testing: The Essential Guide](https://www.browserstack.com/guide/what-is-parallel-testing)

[Parallel Tests Calculator](https://www.browserstack.com/automate/parallel-calculator)

[Docker](https://github.com/lana-20/docker/blob/main/README.md)

[Selenium Grid Tutorial : How to Set It Up](https://www.browserstack.com/guide/selenium-grid-tutorial)

[🖥 💻 Desktop OSs & Browsers - 📊 Market Share & 🎉 Popularity](https://github.com/lana-20/desktop-os-browser-market_share)
