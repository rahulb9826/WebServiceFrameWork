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

Other than these annotations the Framework provide's PDFTool. This Tool generate's two PDF **#### Services.pdf & Errors.pdf**. The Errors PDF tells you about techinical complications. 

## Installation
* Download the repository files (project) from the download section.
* Place the downloaded Jar File(WebServiceFramework.jar) inside WEB-INF/lib of your web application folder. 

# Usage
* Create a Java File inside classes folder of your WebApplication.
* import the **Framework** Package:
``` import com.thinking.machines.Framework.*; ```
## Path
* You need to apply Path annotation over classes and methods which will work as a Servlet. Specify the **url-pattern** to **value** as shown below.
## Forward
## Secured
## Upload
## PDFTool
