## Introduction

This tutorial focuses on deploying BPEL process on Apache ODE.

BPEL, business process execution language, which was written in XML. It is used to automatic process execution, and also known as WSBPEL and BPEL4WS. For more details see [BPEL-Wikipedia](https://en.wikipedia.org/wiki/Business_Process_Execution_Language).

In this tutorial, we need these tools:
- Eclipse for JAVA EE ([Eclipse neon](https://www.eclipse.org/downloads/) and MyEclipse xxx has passed testing, other version maybe work or not.)
- [JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)
- [Apache Tomcat](http://tomcat.apache.org) (8.0 or 8.5)
- [Apache ODE](http://ode.apache.org/getting-ode.html)

OK, here we go.

## Tutorial

First in first, download the Eclipse Java EE, JDK and install it. There are many instruction about this, so ignore it here.

### Install Tomcat and add it in Eclipse
- Download the Tomcat and unzip it. Open Eclipse, Click "Window"-"Show View"-"Servers".
- Right click in the Server window and choose "New"-"Server". 

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/3.PNG)

Choose "Tomcat v8.5 Server" and click "Next", Click "Browse..." and choose the Tomcat directory you have created in the first step. And "Next"... "Finish".

### Install Eclipse BPEL plug-in
Open Eclipse, Click the "Help"-"Install New Software...", input "http://www.mirrorservice.org/sites/download.eclipse.org/eclipseMirror/bpel/site/1.0.5/", and then choose "Eclipse BPEL Designer" and click "Next"..."Accpet xxx" and "Finish".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/1.PNG)

### Install Apache ODE and add it in Eclipse
- Download Apache ODE from [Link](http://ode.apache.org/getting-ode.html) and choose "apache-ode-war-1.3.6.zip".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/2.PNG)

- Unzip the file and copy ode.war into Tomcat/webapps directory and restart the Tomcat. Open the site "http://localhost:8080/ode/" to check if the ode have been successfully deployed. If you see like the picture below, it means finished.

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/4.PNG)

- Open Eclipse, right click in the Server window and choose "New"-"Server". And this time we choose "Ode v1.x Server" and click "Next".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/5.PNG)

- Choose the directory of ODE(xxx/Tomcat/webapps/ode) and Tomcat(xxx/Tomcat). And click "Next"..."Finish".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/6.PNG)

- Double click the Ode server we have added in the Servers window. 

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/7.PNG)

Click "Open launch configuration" and choose "Classpath".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/8.PNG)

Click "User Entries", then "Add External JARs..." and choose the "Tomcat/bin/tomcat-juli.jar" and "Open", "OK".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/9.PNG)

### Create BPEL project in Eclipse
- Open Eclipse, click "File"-"New"-"Other". Find "BPEL 2.0" and choose "BPEL Project".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/10.PNG)

- In "Target runtime", choose "Apache Ode 1.x Runtime". Then "Next", "Finish".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/11.PNG)

- In the project we have created, right click the "bpelContent" and choose "New"-"Other", and select "BPEL Process File". Input the process name and namespace.

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/12.PNG)

In "Template", select "Synchronous BPEL Process" and modify the "Service Address" like "http://localhost:8080/ode/processes/[yourProject]". "Next" and "Finish".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/13.PNG)

### Write a simple BPEL project
After finish the former step, we have created a BPEL project. In this part, we focus on write a simple BPEL process.

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/14.PNG)

- Click the "FIX_ME-Add_Business_Logic_Here" and delete it. Then drag two "Assign" and one "Invoke" module into the process between "receiveInput" and "replyOutput".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/15.PNG)

- Click the "Invoke" and choose "Properties"-"Details". Double click "Create Global Partner Link".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/16.PNG)

- Input a partner link name. Then "OK".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/17.PNG)

- Click "Add WSDL", choose "URL" and input the WSDL address of your service.





Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```


