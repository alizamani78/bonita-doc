# Platform extensibility

Learn how Bonita Platform can be extended to suit your needs.

Bonita provides a rich set of features by default. These features are designed to meet the needs of most of your projects. 
However, if a project has a need that was not anticipated and cannot be met by the default features, Bonita has been designed to be extensible. 
This page lists the extension points that are available.


<a id="stable_extension_points"/>

## Stable extension points

The following elements are designed to be extension points of Bonita. 
These extension points are guaranteed to be stable across versions of Bonita 7: Java interfaces and XML schema will be kept backward compatible so that your implementation will work even after a Bonita version upgrade.

### Connectors

In Community, Teamwork, Efficiency, Performance and Enterprise editions

Bonita comes with more than 80 [standard connectors](_connectivity.md) to the major information system components: major databases (Oracle, Microsoft, Postgres, etc.), SOAP Webservice, Salesforce, Email, etc.
A new connector enables you to provide new connectivity capabilities for processes. 
To [implement a new connector](connectors-overview.md), you need to provide some XML description files and a 
Java class respecting the [Connector interface](http://documentation.bonitasoft.com/javadoc/api/${varVersion}/index.html). 
Connectors can be implemented directly from Bonita Studio.

### Actor filters

In Community, Teamwork, Efficiency, Performance and Enterprise editions

Bonita comes with a set of [standard actor filters](actor-filtering.md) that can be used to reduce the list of candidates for process tasks.
A new actor filter enables you to provide new filtering capabilities to processes. To [implement a new actor filter](creating-an-actor-filter.md), 
you need to provide some XML description files and a Java class respecting the [UserFilter interface](http://documentation.bonitasoft.com/javadoc/api/${varVersion}/index.html). 
Actor filters can be implemented directly from Bonita Studio.

### Engine API

In Community, Teamwork, Efficiency, Performance and Enterprise editions

The [Bonita Engine APIs](http://documentation.bonitasoft.com/javadoc/api/${varVersion}/index.html) enable you to:

* start and stop the engine
* design, install, configure and interact with processes
* manage users

ProcessBuilder and Business Objects DAO are examples of APIs that can be leveraged in your development. They will remain stable in time.

### REST API

In Community, Teamwork, Efficiency, Performance and Enterprise editions

The [REST APIs](rest-api-overview.md) enable you to integrate your Bonita processes into your application and execute operations on Bonita objects including business objects. 
Pages and forms created with the UI designer reply on the REST APIs to manage data.

In addition to the standard APIs and resources, you can define [REST API extensions](rest-api-extensions.md). 
In the Bonita subscription edition, Bonita Studio contains [tooling for creating, testing, and deploying REST API extensions](rest-api-extensions.md).

### Custom pages

In Community, Teamwork, Efficiency, Performance and Enterprise editions

A [custom page](pages.md) is a page that you can add into Bonita Portal to form part of an application, customize information provided in default portal pages, or to add new features to the portal. 
To implement a page, you need to provide HTML, CSS and Javascript resources respecting some packaging constraints. 
You can create a page using the [UI designer](ui-designer-overview.md), which automatically creates a well-formed page. 
Note that although the page framework provided in the product is stable, we cannot guarantee that all custom pages will work with future versions, because this depends on the details of how the page is implemented.

### Custom widgets

In Community, Teamwork, Efficiency, Performance and Enterprise editions

If the standard UI designer [widgets](widgets.md) do not meet your needs, you can create a [custom widget](custom-widgets.md). 
You can then use your custom widget in pages, forms, and (for Subscription editions) fragments.

### Import and export exchange files

In Community, Teamwork, Efficiency, Performance and Enterprise editions

Included in the [Engine APIs](http://documentation.bonitasoft.com/javadoc/api/${varVersion}/index.html) are methods to import and export various items. 
These methods manipulate files with formats that are versioned. Newer versions of the file format are designed to be backward compatible with earlier versions. The following items have import and export API methods:

* organization (users, groups, roles)
* parameters
* custom pages
* connectors

### Authentication service

In Teamwork, Efficiency, Performance and Enterprise editions

From Bonita 6.3, the Engine authentication service is considered to be an official extension point of the solution. It is now safe to provide your own implementation of this service to better fit the needs of your projects.
[Default authentication implementations](user-authentication-overview.md) are provided allow to check user credentials from the Bonita database, LDAP or a CAS SSO server (using JAAS).
To implement an Authentication Service, provide a Java class respecting the Authentication Service interface.

### Event handlers

In Teamwork, Efficiency, Performance and Enterprise editions

An event handler is an extension to the engine that is configured to run when a specified event occurs. An event is a change to any object in the database.
To [implement an event handler](event-handlers.md), you need to provide a Java class respecting the Handler interface.

### BonitaStudioBuilder

::: warning
**Important note**: as of Bonita 7.7.0, the BonitaStudioBuilder tooling (headless studio build) has been deprecated. See the
[Release Notes page](release-notes.md) for more information

We strongly encourage you to use the LA builder included in the tooling suite of Bonita Continuous Delivery add-on. One added-value is that LA builder does not need a studio to be installed.
:::

In Teamwork, Efficiency, Performance and Enterprise editions

Bonita includes a script, BonitaStudioBuilder (also known as the Workspace API), for building a bar file from a process in a project. 
This intended to be used for [automating builds](automating-builds.md) in a continuous integration and testing environment.
You can use the BonitaStudioBuilder to build a bar file for processes stored in a project. 

### Portal look & feel

In Teamwork, Efficiency, Performance and Enterprise editions

The Bonita Portal Look & Feel gives the ability to customize the appearance of the portal Web interface. As a Portal Administrator, you can import a new Look & Feel (.zip archive). 
To [create a new Look & Feel](creating-a-new-look-feel.md), provide CSS and resources files.

### Portal language pack

Bonita Portal comes with a number of language packs by default. You can also [add languages](languages.md). 
It is also possible to use this same mechanism to customize the portal terminology to your business environment. For example, an e-commerce business could change _Cases_ to _Orders_.

### Custom data types

A [custom data type](create-a-complex-data-type.md) is a Java object (.jar file) or an XML definition (.xsd file) of a data structure. 
You can create a custom data type and use it to define a process variable if the standard data types are not suitable for your process. 
Note that although the custom data type framework provided in the product is stable, we cannot guarantee that all custom data types will work with future versions, because this depends on the details of how the data type is implemented.  
From version 7.0, we **strongly recommend** to use the [Business Data capabilities](define-and-deploy-the-bdm.md) instead of custom data types.  

## Unstable extension points

The following elements may be used as extension points but there is no guarantee of stability across versions. No changes are planned, but we reserve the right to change make incompatible changes in any future version.

* **Portal URLs and Forms URLs**. Some customer projects have used hard-coded or forged URLs to access specific pages of Bonita Portal or forms, to fit in with specific technology or navigation constraints. 
While such URLs have so far been quite stable, there is no guarantee that they will not change across Bonita versions. 
Recommendation: if your project relies on such URLs, make URL generation configurable so that you can easily change it if required after a Bonita upgrade.
* **Forms HTML templates**. It is possible to modify the HTML page template, HTML process template, or HTML portal template to customize the appearance and behavior of forms. 
There is no guarantee that these templates will not change across Bonita versions. 
If a form uses some Javascript code based on an element in the HTML Document Object Model, the element may be moved, modified or removed in a future version so the Javascript will no longer work.
* **Authorization Rule Mapping**. It is possible to modify authorization rules mapping applied to start a process, display process overview or execute a task. 
You can customize this mapping by defining your own bean and override property. See [Authorization Rule Mapping](custom-authorization-rule-mapping.md)   
* **BonitaStudioBuilder**
Bonita Entreprise editions include a script, BonitaStudioBuilder (also known as the Workspace API), for building a bar file from a process in a project. This intended to be used for automating process builds in a continuous integration and testing environment. You can use the BonitaStudioBuilder to build a bar file for processes stored in a project. 
WorkspaceAPI is deprecated since Bonita 7.7.0. Instead, we strongly encourage you to use the *LA builder* included in the tooling suite of [*Bonita Continuous Delivery* add-on](https://documentation.bonitasoft.com/bcd/2.0/). One added-value is that LA builder does not need a Studio to be installed.
 
Only the elements listed on this page are intended to be used as extension points. For other elements, there is no guarantee of stability, and a high probability of changes across versions. 
For example, the following should not be considered to be extension points:

* **Engine Services** (other than those listed in this page). The Engine is structured as an aggregation of several services. 
This provides clear isolation of responsibility and eases maintenance. The interfaces, configuration files, and existence of services are not guaranteed across versions.

## Backward compatibility

In Bonita 7.x, we ensure backward compatibility of the following:

* Engine API (except items marked as deprecated)
* Web REST API (except items marked as deprecated)
* Authentication Service (from 6.3.0 onwards)
* XML file format for the following:
  * event handlers
  * BonitaStudioBuilder (also known as the Workspace API)
  * actor filters
  * connectors
  * form validators
  * import and export exchange files

We cannot ensure backward compatibility for the following:

* Portal Look & Feel definition structure
* Custom Pages definition structure
* Custom data types definition structure
* URLs
* Forms definition structure and HTML templates
* bonita home folder structure and content (removed since 7.3)
