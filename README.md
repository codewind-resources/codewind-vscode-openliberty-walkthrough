# Codewind Quicklab

Moving workloads to the cloud introduces a steep learning curve for developers accustomed to traditional web application development. Cloud-native applications are usually containerized (either Docker or OCI containers) and are run on orchestrated platforms like Kubernetes. These are complex technologies that bring big changes to the development workflow. Can this be simplified? Can developers create cloud-native applicatioons and deploy them to Kubernetes without climbing the mountainous learning curve? 

In this quicklab we will take a look at a use case involving Eclipse Codewind, a technology that simplify development of containerized cloud-native applications. Codewind is an IDE plugin that allows you to work with containerized applications in a familiar way. With Codewind, developers can start building cloud-native applications like experts without having to be an expert in all the cloud-native technologies. 

## Prerequistes

If you're running this lab on your own laptop, make sure you have a few things already installed.

<details>
  <summary>Click to expand</summary>
  
### Configure Local System

This quicklab requires the following tools: 

1. Docker
2. VS Code
3. VS Code Codewind [extension](https://www.eclipse.org/codewind/mdt-vsc-getting-started.html)

We recommend working with the latest available version of each.

</details>

# Improving Developer Productivity with Eclipse Codewind

[Eclipse Codewind](https://www.eclipse.org/codewind/) is a plugin for IDEs, currently available in VS Code, Eclipse, and Eclipse Che, that helps improve developer productivity when developing containerized applications. Let's explore how Codewind can help you be a more productive developer.

1. Open VS Code (on the Mac, press **command** + **space bar** and type "code" into the dialog box)
2. In the explorer window under **CODEWIND** click on the "**+**" to create a new project
![Show user how to create a new project](https://raw.githubusercontent.com/beccabau/codewind-vscode-openliberty-walkthrough/master/images/codewind-explorer.png)

3. In the dialog pop-up search for "Open Liberty" and select the "Open Liberty (Default templates)" option
![Show user how to find and select an Open Liberty template](https://raw.githubusercontent.com/beccabau/codewind-vscode-openliberty-walkthrough/master/images/search-project-type.png)

4. Enter **cloud-native-microprofile** as the project name and hit enter. You will see a dialogue asking what parent directory you want for your projects. For the purposes of this lab, create a "codewind-workspace" directory during this step (if it does not already exist). In reality, you can choose to place the projects wherever it makes sense for you.
	![name your project](https://raw.githubusercontent.com/beccabau/codewind-vscode-openliberty-walkthrough/master/images/create-project.png)
  
# Automated Code Reload

A key to increasing developer productivity is shortening and reducing the friction in the feedback loop. Codewind improves your inner loop experience, enabling you to create a microservice quickly, rapidly iterate on changes and make improvements to performance. As you develop, Codewind *automatically* pushes your code changes to your container as efficiently as possible. 

Let's look at this feature in action.

1. 	In the project workspace under **src/main/java/io/openliberty/sample** create a new file **HelloResource.java**
![Create a file called HelloResource.java](https://raw.githubusercontent.com/beccabau/codewind-vscode-openliberty-walkthrough/master/images/create-hello-dot-java.gif)
2. Edit **HelloResource.java** to look like below:
	
```
package io.openliberty.sample;

import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.ws.rs.Produces;
import javax.ws.rs.core.MediaType;
import javax.ws.rs.core.Response;
import javax.ws.rs.QueryParam;

import java.awt.*;

@Path("/hello")
public class HelloResource {

    @GET
    @Produces(MediaType.TEXT_PLAIN)
    public Response hello(@QueryParam("name") String name) {
        
        return Response.ok( "Hello " + name).build();

    }

}
```

3. You can view the status of the re-build and re-deploy by looking at the status indicator next to the project under the Codewind context. Once status returns to [Running][Build Suceeded] you can refresh your browser window to view the change we made. Please be aware that it can take a few seconds until something happens. 
	![See app status](https://raw.githubusercontent.com/beccabau/codewind-vscode-openliberty-walkthrough/master/images/app-status.png)	
4. In VS Code click the "Open Application" icon.	
5. Append `/system/hello?name=Cloud Native Microprofile` to the end of the url. You can try adding your own name next time.
    ![append url to see your example work](https://raw.githubusercontent.com/beccabau/codewind-vscode-openliberty-walkthrough/master/images/append-url.gif)


# View the Performance Dashboard

You can run an application and use the performance dashboard data to determine whether the application is working harder than it should. By determining which applications are running harder than necessary, the performance dashboard can help you find slower applications and detect memory leaks.

You'll notice that if you try to run a load test with the default project configuration, you will not get any results on the performance dashboard. This is because not all projects will have the required packages needed to provide monitoring, Spring Boot being one of these projects. However, we provide the ability to auto inject the required configuration at build time to include these packages. You will need to opt in for this to happen as it will modify the source code (but only in the build container).

1. Navigate to the Project Overview page. You can do this either by right-clicking on the project in the Codewind explorer and selecting "Open Project Overview" or simply click the (i) information icon. 
    ![](https://raw.githubusercontent.com/beccabau/codewind-vscode-openliberty-walkthrough/master/images/open-proj-overview.png)
2. Enable "Inject metrics." 
    ![](https://raw.githubusercontent.com/beccabau/codewind-vscode-openliberty-walkthrough/master/images/inject-metrics.gif) 
Wait for the Application Status to go back to Running - it shouldn't take long.
3. When the status reflects **[Running][Build Succeeded]** Navigate to the Performance Dashboard. ![](https://raw.githubusercontent.com/beccabau/codewind-vscode-openliberty-walkthrough/master/images/open-perf-dashboard.png)
4. Now you can run a load test and monitor your application. 
    ![](https://raw.githubusercontent.com/beccabau/codewind-vscode-openliberty-walkthrough/master/images/perf-dash.gif)

# Other Actions
## View the Application Monitor
Opening the Application monitor allows you to monitor the activity and health of your application. This action is only available when the application is running or debugging.
![](https://raw.githubusercontent.com/beccabau/codewind-vscode-openliberty-walkthrough/master/images/open-metrics-dash.gif)

## View Application Logs

Viewing the logs of your application running in a docker container is easy from the IDE with Codewind. 

To view the logs for an application, right click on it and select "Show All Logs" 

![](https://raw.githubusercontent.com/beccabau/codewind-vscode-openliberty-walkthrough/master/images/show-logs.gif)

The logs for the running application will be shown in the IDE console log window on the bottom right of the page. 

<!---
[//]: # Resources
[//]: # https://openliberty.io/guides/
[//]: # https://www.youtube.com/watch?v=PnHT4ld0w18
[//]: # http://www.adeveloperdiary.com/java/webservice/rest/how-to-configure-rest-service-jax-rs-in-ibm-liberty-profile/
[//]: # #codewind-vscode-ol-microprofile-quicklab
[//]: # https://labs.cognitiveclass.ai/tools/theiadocker/?md_instructions_url=https://raw.githubusercontent.com/beccabau/codewind-vscode-ol-microprofile-quicklab/master/README.md
---!>
# codewind-vscode-openliberty-walkthrough
