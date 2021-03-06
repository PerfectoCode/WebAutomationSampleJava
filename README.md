# Java + TestNG Web Automation Code Sample

This code sample demonstrates how to use Perfecto Web Machines & Selenium + TestNG in order to execute tests 
for your web applications on the cloud. 

### Quick Start: 
- Clone or download the sample:<br/> `git clone https://github.com/PerfectoCode/WebAutomationSampleJava.git`
- Add your Perfecto Lab credentials within the [Utils.java](src/test/java/Utils.java) class:
```Java
...
private static final String token = System.getenv("token");
private static final String host = System.getenv("host");
... 
```
You may want to use env variable for your credentials as demonstrated.

Old school credentials may be used (for non turbo web only) by replacing the security token with username and password:
```Java
...
private static final String user = System.getenv("user");
private static final String password = System.getenv("password");
...
```
:exclamation:Using old school credentials is not a best practice and is not recommended.

- Note:exclamation: the project include 2 templates:
    - PerfectoFastWebTemplate: template for Perfecto Turbo Web.
    - PerfectoFastWebTemplateReporting: template for Perfecto Turbo Web + DigitalZoom Reporting.
- Choose one (or more) of the templates, add it's class name in the [testng.xml](testng.xml) file for example:
```xml
<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd" >
<suite name="Suite1" verbose="1" >
    <test name="Fast Web" >
        <classes>
            <class name="PerfectoFastWebTemplate" />
        </classes>
    </test>
</suite>
```
In the example above we use the PerfectoFastWebTemplate.

- Run the project with the gradle command: `./gradlew WebSample` Where the WebSample argument denote the task responsible to run the test.
Otherwise, use the testng.xml via your IDE to execute the tests without using the command line. 

### Web Capabilities: 
- To insure your tests run on Perfecto Web machines on the cloud use the capabilities as demonstrated in the code sample: <br/>
```Java
@BeforeMethod
void beforeMethod() throws MalformedURLException {

    DesiredCapabilities capabilities = new DesiredCapabilities();
    capabilities.setCapability("platformName", "Windows");
    capabilities.setCapability("platformVersion", "10");
    capabilities.setCapability("browserName", "Chrome");
    capabilities.setCapability("browserVersion", "latest");
    capabilities.setCapability("resolution", "1280x1024");
    capabilities.setCapability("securityToken", Utils.Capabilities.getToken());

    //In case of old school credentials replace security token with:
    //capabilities.setCapability("user", Utils.Capabilities.getUser());
    //capabilities.setCapability("password", Utils.Capabilities.getPassword());
    
    // ... Rest of the code in beforeMethod()
}
```

- More capabilities are available, read more [here](http://developers.perfectomobile.com/display/PD/Supported+Platforms).

### Perfecto Turbo Web Automation:

Perfecto's Desktop Web environment introduces an accelerated interface to Web Browser automation with its new Turbo web interface. Using this new environment will allow you to connect quicker to the browser "device" you select for automating and testing your web application.

*Click [here](http://developers.perfectomobile.com/display/PD/Automating+Web-apps+with+Perfecto) to read more about Turbo Web Automation.*

- To enable Turbo Web Automation in this code sample follow the instructions in the link above in order to generate authentication token.
Place the authentication token within the [Utils.java](src/test/java/Utils.java) class:
```Java
private static final String token = System.getenv("token");
```

### Perfecto DigitalZoom reporting:

Perfecto Reporting is a multiple execution digital report, that enables quick navigation within your latest build execution. Get visibility of your test execution status and quickly identify potential problems with an aggregated report.
Hone-in and quickly explore your test results all within customized views, that include logical steps and synced artifacts. Distinguish between test methods within a long execution. Add personalized logical steps and tags according to your team and organization.

*Click [here](http://developers.perfectomobile.com/display/PD/Reporting) to read more about DigitalZoom Reporting.*
