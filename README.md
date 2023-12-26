# Soap Webservices

## Overview
* Reference: https://www.udemy.com/course/java-web-services/learn/lecture/2174106#overview
* Webservices applications have consumer and provider and these re decoupled and can be developed in different languages.
* Webservices are of 2 types
  * SOAP : This uses XML and HPP POST
  * RESTFul: This is more powerful and uses multiple data formats and http methods
* In java world, teh frameworks are:
  * JAX-WS: For SOAP services
  * JAX-RS: FOR REST services

## SOAP (Simple Object Access Protocol)
* The contract between consumer and provider services is specified in the WSDL file. WSDL stands for Web Services Description Language
* A WSDL file has an abstract part and a physical part
* The abstract part says what the SOAP server will provide
  * definitions
    * types
    * messages
    * operations
    * porttype
* The physical part says how teh SOAP server will provide this service
  * binding
  * service
* The SOAP binding has multipe styles. 3 things change based on this style
  * First style is <binding style="document/literal">
  * First style is <binding style="document/encoded">
  * First style is <binding style="RPC/literal">
  * First style is <binding style="RPC/encoded">
* The things that change based on style are
  * SOAP Payload
  * Validation
  * Operation Name SOAP Message
* The style to use is explained here by IBM: https://developer.ibm.com/articles/ws-whichwsdl/

## SOAP Webservice Design Approach
* Create WSDL first and then the code
* Create Code first and then genearte WSDL file

### Create WSDL first approach
* Create the WSDL file
* Generate the java stubs using tools like wsdl2java
* Implement the web services endpoint

### Create code first approach
* Create code first and annotate
* Genearte the wsdl from code using tools like java2wsdl

## JAX-WS
* The framework has Specification and API
* The specification is implemented by engines like Aapxhe CXF, Glassfish, Apache Axis
* The API contains annotations that we sue in servcie provider and consumer like:
  * @javax.jws.WebService (this tells the engines that this class is an endpoint)
  * @javax.jws.WebMethod
  * @WebParam
  * @WebResult
  * @javax.xml.ws.WebFault
  * @javax.jws.soap.SOAPBinding (style=Style.RPC, use=Use.LITERAL)
  * @javax.xml.ws.RequestWrapper
  * @javax.xml.ws.ResponseWrapper
```
@javax.jws.WebService
public class OrderService{

  @javax.jws.WebMethod
  @WebResult(name = "order") Order getOrder( @WebParam(name = "orderId") Long orderId) {

  }
}

@javax.xml.ws.WebFault
public class MyException exetnds Exception {

}
```

## JAXB Specification
* Java API for XML Binding
* A reference implementation of JAXB comes with jdk 1.6 and greater
* JAXB is internally used by SOAP engines like Apache CXF
* Provides easy way to convert XML schema to Java Objects and vice-versa
* The spec provides 3 tools:
  * XJC: converts xml schema to Java class. This is inside $JAVA_HOME/bin
  * SCHEMAGEN: converts java class to xml schema. This is inside $JAVA_HOME/bin
  * Runtime API: marshals and unmarshals xml and java class at runtime and also provides annotations
* Although we can directly use xjc/schemagen on teh command, usually we use the build tool's plugin like org.jvnet.jaxb2.maven2 plugin of maven

## Apache CXF
* It supports Spring Boot
* Add the dependency cxf-spring-boot-starter-jaxws
* Add a property in application properties called cxf.jaxrs.component-scan=true. With this property, all webservices endpoint will be discovered snd published
* 
