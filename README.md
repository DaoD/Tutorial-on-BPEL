## Introduction

This tutorial focuses on deploying a BPEL process on Apache ODE.

BPEL, i.e., business process execution language, is written in XML. It is used to achieve automatic process execution, and also known as WSBPEL and BPEL4WS. For more details, please refer to [BPEL-Wikipedia](https://en.wikipedia.org/wiki/Business_Process_Execution_Language).

In this tutorial, we need these tools:
- Eclipse for JAVA EE ([Eclipse neon](https://www.eclipse.org/downloads/) and MyEclipse 2017 CI 1 has passed test, other version maybe work or not.)
- [JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)
- [Apache Tomcat](http://tomcat.apache.org) (8.0 or 8.5)
- [Apache ODE](http://ode.apache.org/getting-ode.html)
- [Axis2](http://axis.apache.org/axis2/java/core/download.cgi)

OK, here we go.

## Tutorial

Firstly, download the Eclipse Java EE, JDK and install it. There are many instructions about this step, so it is ignored here.

### Install Tomcat and add it in the Eclipse
- Download the Tomcat and unzip it. Open the Eclipse, and click "Window"-"Show View"-"Servers".
- Right click the Server window and choose "New"-"Server". 

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/3.PNG)

Choose "Tomcat v8.5 Server" and click "Next". Click "Browse..." and choose the Tomcat directory we have created in the first step. And click "Next"... "Finish".

### Install the Eclipse BPEL plug-in
Open Eclipse, and click the "Help"-"Install New Software...". Input "http://www.mirrorservice.org/sites/download.eclipse.org/eclipseMirror/bpel/site/1.0.5/", and then choose "Eclipse BPEL Designer" and click "Next"..."Accpet xxx" and "Finish".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/1.PNG)

### Install Apache ODE and add it in the Eclipse
- Download the Apache ODE from [Link](http://ode.apache.org/getting-ode.html) and choose "apache-ode-war-1.3.6.zip".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/2.PNG)

- Unzip the file and copy ode.war into Tomcat/webapps directory and restart the Tomcat. Open the site "http://localhost:8080/ode/" to check if the ODE has been successfully deployed. If everything goes well, you can see the scene like the picture below.

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/4.PNG)

- Open the Eclipse, right click in the Server window and choose "New"-"Server". Choose "Ode v1.x Server" and click "Next".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/5.PNG)

- Choose the directory of ODE (xxx/Tomcat/webapps/ode) and Tomcat (xxx/Tomcat). And click "Next"..."Finish".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/6.PNG)

- Double click the ODE server we have added in the Servers window. 

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/7.PNG)

Click "Open launch configuration" and choose "Classpath".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/8.PNG)

Click "User Entries", then click "Add External JARs..." and choose the "Tomcat/bin/tomcat-juli.jar" and "Open", "OK".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/9.PNG)

### Create BPEL project in Eclipse
- Open the Eclipse, click "File"-"New"-"Other". Find "BPEL 2.0" and choose "BPEL Project".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/10.PNG)

- In "Target runtime", choose "Apache Ode 1.x Runtime". Then click "Next", "Finish".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/11.PNG)

- In the project we have created, right click the "bpelContent" and choose "New"-"Other", and select "BPEL Process File". Input the process name and namespace. Here exsits a small bug, we need to set the namespace as the service we invoke. Otherwise, an error may occur.

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/12.PNG)

- In "Template", select "Synchronous BPEL Process" and modify the "Service Address" like "http://localhost:8080/ode/processes/[yourProject]". Click "Next" and "Finish".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/13.PNG)

### Write a simple BPEL project
After finishing the former steps, we have created a BPEL project. In this part, we focus on writing a simple BPEL process.

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/14.PNG)

- Click the "FIX_ME-Add_Business_Logic_Here" and delete it. Then drag two "Assign" and one "Invoke" modules into the process between "receiveInput" and "replyOutput".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/15.PNG)

- Click "Invoke" and choose "Properties"-"Details". Double click "Create Global Partner Link".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/16.PNG)

- Input a partner link name. Then click "OK".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/17.PNG)

- Click "Add WSDL", choose "URL" and input the WSDL address of our service. Choose the service in the WSDL which we want to invoke. Then input the name and role name. Click "Finish".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/18.PNG)
![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/19.PNG)

- In the properties-detail window, pick the function we want to invoke in the right side "Quick Pick". Double click it and it will create input variables and output variables automaticlly. In this step, we define the service we want to use.

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/20.PNG)

- Click the first assign module. In the properties-detail window, click "New" and choose "From" and "To" respectively. 

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/21.PNG)

After this, the Eclipse will prompt "if you need a initializer for these assignments". Choose "Yes".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/22.PNG)

In this step we assign the BPEL input to the parameters of the function we invoke. But be careful, sometimes the Eclipse will not generate initializer automatically although we have choosed "yes" in the former step. Under this circumstance, we need to initialize it manually. Just edit the XML file like the picture. Choose "Fixed Value" and write "ns:<functionname> and ns:<parametername>". And click parameters under the Request in the "To" variable window. It means use the fixed value to initialize the parameters.

- Click the second assign module. And do the same things as aforementioned. But pay attention to the "From" and "To". This time we assign the response to output. And an initializer is essential like the former step.

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/23.PNG)

- Click the "xxxxxArtifacts.wsdl". This file is generated automatically by the Eclipse. Open it and click "Source". Move down to the tail. And modify the soap:address location. This address is the same as we input in service address. It is an easy way to deploy BPEL in ODE because we write /ode/processes/[yourProject] here.

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/24.PNG)

- After these steps, our BPEL process is created. Then we need to deploy it. Right click the bpelContent and choose "New"-"Other", choose "BPEL Deployment Descriptor" and "Finish".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/25.PNG)

- In the deploy.xml, choose client "Associated port". This is the BPEL port itself. Then choose a partner link "Associated port", and this point to which soap port we invoke the service. After the selection, do not forget to save it.

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/26.PNG)

- We have finished all of the BPEL process. And let's test it now. Right click ODE server in the Server window, then choose "Add and Remove...". Choose the project we have created and add it into the server, then click "OK".

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/27.PNG)

- Then we test the BPEL process. Right click the "xxxxxArtifacts.wsdl" and "Web Services"-"Test with Web Services Explorer". Click the "process" and input the value we want to test.

![Image](https://github.com/DaoD/Tutorial-on-BPEL/raw/master/images/28.PNG)

- If everything goes well, we can get the result. Hint: If you invoke more than one service (import more than one WSDL) in one BPEL, the Eclipse will prompt "Duplicate key value declared for identity constraint import of element definitions" error, it doesn't matter and I guess there is something wrong in Eclipse BPEL code check system. Besides, if the service you invoke in the WSDL doesn't have a return value, it will prompt another problem. Just ignore it :)

### Test BPEL by Java
We can also test the BPEL process by Java. In fact, it is the same way to invoke a wsdl process.

- Import relatd packages, and these packages can be found in axis2/lib directory.

```java
import javax.xml.namespace.QName;
import org.apache.axiom.om.OMAbstractFactory;  
import org.apache.axiom.om.OMElement;  
import org.apache.axiom.om.OMFactory;  
import org.apache.axiom.om.OMNamespace;
import org.apache.axiom.om.OMNode;
import org.apache.axis2.AxisFault;  
import org.apache.axis2.addressing.EndpointReference;  
import org.apache.axis2.client.Options;  
import org.apache.axis2.client.ServiceClient;  
import org.apache.axis2.rpc.client.RPCServiceClient;
```

- Invoke the BPEL or WSDL.

```java
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
