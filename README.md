# WebServiceFrameWork
Framework to provide vantage for Servlet programming.

## Description
As we know that to handle requests for Webpages we need to create Servlets on backend & a lot of code of this servlets is similar for all, like creating **doGet, doPost** methods and retriving the data sent from FrontEnd by user. So, to create simplicity for Servlet programming, I created a **WebServiceFramework** to handle the requests from front-end & perform whatever needs to be performed. The back-end programmer just need to create **Java Classes & Methods** having some required annotations on them.

## Features
The Framework works with the usage of some annoatations which are to applied on the classes & methods. The Annotations are:
* **Path Annotation-** The Path Annotation is a single value annotation having one member named as value. This annotation defines the **url-pattern** of your Java classes & methods.  
* **Secured-** The Secured annotation is used for performing certain validations which will decide whether the body is to be evaluated or not.
* **Forward-** The Forward annotation provide functionality to redirect it a jsp page or method of same class after the execution of this method.
* **Upload-** The Upload is a Marker annotation which is is used for the methods that requires uploading of Files.

Other than these annotations the Framework provide's PDFTool. This Tool generate's two PDF **Services.pdf & Errors.pdf**. The Errors PDF tells you about techinical complications. 

## Installation
* Download the repository files (project) from the download section.
* Place the downloaded Jar File(WebServiceFramework.jar) inside WEB-INF/lib of your web application folder. 

## Usage
* The Front-end devloper needs to request for Servlet using AjaxType as the framework is commited for AJAX request. The framework expects JSON String as recieved data, which will be passed to the method accordingly.

* The Back-end devloper need to map **Framework** servlet in web.xml to load-on-startup. An another mapping for **Services** servlet is required which will call the requested class and it's method from requested URL. The code is shown below:

**Framework Mapping**
```
<servlet>
<servlet-name>Framework</servlet-name>
<servlet-class>com.thinking.machines.framework.Framework</servlet-class>
<load-on-startup>0</load-on-startup>
</servlet>
```
**Services Mapping**
```
<servlet>
<servlet-name>Services</servlet-name>
<servlet-class>com.thinking.machines.framework.Services</servlet-class>
</servlet>
<servlet-mapping>
  <servlet-name>Services</servlet-name>
  <url-pattern>/services/*</url-pattern>
</servlet-mapping>
```

* The Back-end devloper also needs to create a file named as **```Config.conf```** inside the WebApplication folder parallel to **WEB-INF** folder. The File will contain the name of the packages of the Services(class files). The package name must be written in **JSON Array** format named as **packageNames**. An Example is shown below:
```
{"packageNames":["com.example1.abcd","com.example2.pqr"]}
```

* Create a Java File inside classes folder of your WebApplication.
* import the **Framework** Package:
``` import com.thinking.machines.Framework.*; ```
To use a Class & Method as Servlet you need to specify Path annotation on them.

**Parameters for Methods**: The method can request following objects as parameters:
* **HttpServletRequest**
* **HttpServletResponse**
* **HttpSession**
* **ServletContext**
* **ResponseString**

Here ResponseString specifies the data recieved from the webpage.

## Path
You need to apply Path annotation over classes and methods which will work as a Servlet. Specify the **url-pattern** to **value** as shown below.
```
import com.thinking.machines.framework.Path;

@Path(value="/example")
public class example
{
  @Path(value="/abcdURL")
  public void abcd(ExampleBean exampleBean,ServletContext servletContext)
  {
  //do your stuff
  }
 }
```

## Forward
The Forward annotation can be used over any method which you want to either redirect to certain webpage or to any other Method of same class. Specify the value of **url** property in which you have to specify **webpage/Servlet** name. The framework will invoke the requested method & than will redirect to provided **Webpage/Servlet**. A snippet of it's usage is shown below:

```
import com.thinking.machines.framework.Forward;
import com.thinking.machines.framework.Path;

@Path(value="example")
public class example
{
  @Path(value="/abcdURL")
  @Forward(url="abcd.html")
  public void abcd(ExampleBean exampleBean,ServletContext servletContext)
  {
  //do your stuff
  }
  @Path(value="/pqrURL")
  @Forward(url="servletName")
  public String pqr(ExampleBean exampleBean,ServletContext servletContext)
  {
  //do your stuff
  }
 }
```

## Secured
The Secured annotation can be used to perform certain validations before performing the requested method. For this the programmer needs to create a Class which will impliment **WebServiceFramework** & will override **Authenticate** method. A snippet for expected class is 
shown below.

```
import com.thinking.machines.framework.WebServiceFramework;

public class ValidationClass implements WebServiceFramework
{
  public boolean Authenticate(HttpSession session,HttpServletRequest request,HttpServletResponse response)
  {
    //do whatever you want
  }
}

```
**For annotation usage**
```
import com.thinking.machines.framework.Upload;
import com.thinking.machines.framework.path;

@Path(value="/abcdURL")
  @Secured(service="ValidationClass") //service value must match the name of class implimenting WebServiceFramework
  public void abcd(Files[] filesArray,HttpServletResponse response)
  {
  //do your stuff
  }
  ```
  
The method will return true/false. The devloper needs to ensure that the method must retrun true only if the validations applied by him are true. The method will execute only if the Authenticate returns true.

## Upload
If you want to upload files on the server side than you have to specify **Upload** annotation on the method. The Framework will provide an array of File type which needs to recieved as parameter by the method. A snippet of annotation usage is shown below:

```
import com.thinking.machines.framework.Upload;
import com.thinking.machines.framework.path;

@Path(value="/abcdURL")
  @Upload
  public void abcd(Files[] filesArray,HttpServletResponse response)
  {
  //do your stuff
  }
```

## PDFTool
The **PDFTool** creates PDF of the Services the BackEnd devloper has created. If there are some technical complications in the Services
like two methods with same value of Path annotation, then it will create another PDF as **Errors.pdf** which will contain the methods having error. To use the **PDFTool** use following line in **cmd**.

``java -cp c:\tomcat9\webapps\``**``webapplication``**``\WEB-INF\lib\*;c:\tomcat9\lib\*; com.thinking.machines.framework.PDFTool``

Change the path of lib folder of tomcat9 accordingly.

