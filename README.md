## Introduction

This tutorial focuses on deploying BPEL process on Apache ODE.

BPEL, business process execution language, which was written in XML. It is used to automatic process execution, and also known as WSBPEL and BPEL4WS. For more details see [BPEL-Wikipedia](https://en.wikipedia.org/wiki/Business_Process_Execution_Language).

In this tutorial, we need these tools:
- Eclipse for JAVA EE ([Eclipse neon](https://www.eclipse.org/downloads/) and MyEclipse xxx has passed testing, other version maybe work or not.)
- [JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)
- [Apache Tomcat](http://tomcat.apache.org) (8.0 or 8.5)
- [Apache ODE](http://ode.apache.org/getting-ode.html)
- [Axis2](http://axis.apache.org/axis2/java/core/download.cgi)

OK, here we go.

## Tutorial

First in first, download the Eclipse Java EE, JDK and install it. There are many instruction about this, so ignore it here.

### Install Tomcat and add it in Eclipse
- Download the Tomcat and unzip it. Open Eclipse, Click "Window"-"Show View"-"Servers".
- Right click in the Server window and choose "New"-"Server". 

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/3.PNG)

Choose "Tomcat v8.5 Server" and click "Next", Click "Browse..." and choose the Tomcat directory we have created in the first step. And "Next"... "Finish".

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

- In the project we have created, right click the "bpelContent" and choose "New"-"Other", and select "BPEL Process File". Input the process name and namespace. Here exsits a small bug, we need to set the namespace as the service we invoke. Otherwise, may be an error occured.

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/12.PNG)

- In "Template", select "Synchronous BPEL Process" and modify the "Service Address" like "http://localhost:8080/ode/processes/[yourProject]". "Next" and "Finish".

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

- Click "Add WSDL", choose "URL" and input the WSDL address of our service. Choose the service in the WSDL which we want to invoke. Then input the name and role name. "Finish".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/18.PNG)
![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/19.PNG)

- In the properties-detail window, pick the function we want to invoke in the right side "Quick Pick". Double click it and it will create input variable and output variable automaticlly. This step defines which service we want to use.

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/20.PNG)

- Click the first assign module. In the properties-detail window, click "New" and choose From and To respectively. 

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/21.PNG)

After this, Eclipse will prompt if you need a initializer for these assignments. Choose Yes.

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/22.PNG)

In this step we assign the BPEL input to the parameters of the function we invoke. But be careful, sometimes the Eclipse will not generate initializer automatically although we choose "yes". Under this circumstance, we need to initialize it manually. Just write the xml like the picture. Choose "Fixed Value" and write "ns:<functionname> and ns:<parametername>". And click parameters under the Request in the To variable window. It means use the fixed value to initialize the parameters.

- Click the second assign module. And do the same things as before. But pay attention to the From and To. This time we assign the response to output. And a initializer is essential like the former step.

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/23.PNG)

- Click the "xxxxxArtifacts.wsdl", this file is generated automatically by Eclipse. Open it and click "Source". Move down to the tail. And modify the soap:address location. This address is the same as we input in service address. It is an easy way to deploy BPEL in ode because we write /ode/processes/[yourProject] here.

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/24.PNG)

- After these steps, our BPEL process finished. Then we need to deploy it. Right click the bpelContent and choose "New"-"Other", choose "BPEL Deployment Descriptor" here and "Finish".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/25.PNG)

- In the deploy.xml, choose client "Associated port", this is the BPEL port itself. And choose partner link "Associated port", this point to which soap port we invoke the service. After selection, do not forget save it.

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/26.PNG)

- We have finish all of the BPEL process. And let's test it now. Right click Ode server in the Server window, choose "Add and Remove...". Choose the project we have created and add it into the server, then click "OK".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/27.PNG)

- Then we test the BPEL process. Right click the "xxxxxArtifacts.wsdl" and "Web Services"-"Test with Web Services Explorer". Click the "process" and input the value we want to test.

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/28.PNG)

- If everything worked successfully, we will get the result.

### Test BPEL by Java
We can also test the BPEL process by Java. In fact, it is the same way to invoke a wsdl process.

- Import relatd packages, these packages you can find in axis2/lib directory.
```markdown
`import javax.xml.namespace.QName;  
import org.apache.axiom.om.OMAbstractFactory;  
import org.apache.axiom.om.OMElement;  
import org.apache.axiom.om.OMFactory;  
import org.apache.axiom.om.OMNamespace;
import org.apache.axiom.om.OMNode;
import org.apache.axis2.AxisFault;  
import org.apache.axis2.addressing.EndpointReference;  
import org.apache.axis2.client.Options;  
import org.apache.axis2.client.ServiceClient;  
import org.apache.axis2.rpc.client.RPCServiceClient;`
```

- Invoke the BPEL or WSDL
```markdown
OMElement result = null;  
try {  
    String url = "http://localhost:8080/ode/processes/BPELSayHello?wsdl"; //BPEL or WSDL address

    Options options = new Options();   
    EndpointReference targetEPR = new EndpointReference(url);  
    options.setTo(targetEPR);  

    ServiceClient sender = new ServiceClient();  
    sender.setOptions(options);  

    OMFactory fac = OMAbstractFactory.getOMFactory();  
    String tns = "http://fabu"; //the same as the BPEL or WSDL namespace

    OMNamespace omNs = fac.createOMNamespace(tns, "");

    OMElement method = fac.createOMElement("BPELSayHelloRequest", omNs); //which function you want to invoke

    OMElement symbol1 = fac.createOMElement("input", omNs); //define the parameter name
    symbol1.addChild(fac.createOMText(symbol1, "123")); //define the parameter value
    method.addChild(symbol1);

    method.build();
    System.out.println(method);
    result = sender.sendReceive(method);

    //Get the result by loop
    Iterator iterator =  result.getChildElements();
    while (iterator.hasNext()) {
      OMElement omNode = (OMElement) iterator.next();
      Iterator iterator2 = omNode.getChildElements();
      while(iterator2.hasNext()) {
        OMElement omNode2 = (OMElement) iterator2.next();
        System.out.println(omNode2.getLocalName() + ": " + omNode2.getText());
      }
      System.out.println();

    }

    System.out.println(result);  

} catch (AxisFault axisFault) {  
    axisFault.printStackTrace();  
}  
```


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


