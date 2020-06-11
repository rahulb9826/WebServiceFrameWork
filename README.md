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
The Back-end devloper need to map **Framework** servlet in web.xml to load-on-startup. An another mapping for **Services** servlet is required which will call the requested class and it's method from requested URL. The code is shown below:

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

## Forward
The Forward annotation can be used over any method which you want to either redirect to certain webpage or to any other Method of same class. Specify the value of **url** property in which you have to specify **webpage/Servlet** name. The framework will invoke the requested method & than will redirect to requested **Webpage/Servlet**.

## Secured

## Upload
If you want to upload files on the server side than you have to specify **Upload** annotation on the method. The Framework will provide an array of File type which needs to recieved as parameter by the method.

## PDFTool
