---
layout: post
title:  "Swagger documentation customisation"
date:   2017-11-21
author: francesco
categories: documentation
---

[Swagger][1] is a popular software framework that helps developers build RESTful Web services through their entire lifecycle, from design and documentation, to test and deployment. 
This post focuses on how to incorporate the API documentation generated through Swagger inside an HTML page hosted from another web application.

One of the main features of Swagger is producing interactive documentation for a RESTful API. Swagger can be used in conjunction with a multitude of different languages and frameworks.
It will always produce two different outputs inside the same web application hosting the API:

 1. A default HTML page having a standard Swagger style. ([Europe PMC Annotations API Swagger standard html page] [2])
 2. A JSON file that will contain the description of the generated documentation ([Europe PMC Annotations API documentation descriptor][3])

The goal is to display the Swagger HTML documentation inside an external web site page adapting Swagger's default style to the one of the external site. 
One option could be to copy manually the HTML produced from Swagger inside the external site page. The obvious disadvantage of this solution is that it will be necessary to keep the Swagger code contained into the RESTful API web application in sync with the content shown in the external page, each time a modification to the documentation is performed.
Ideally the content of the Swagger documentation should be displayed in the external page loading it dynamically from the RESTful API application, to avoid synchronization issues.
To this end it is necessary to perform the following steps:

 - Download the Swagger UI folder from: [GitHub][4]
 - Once downloaded, create a swagger-ui folder in the resources folder of the external web application and add the contents downloaded from the Github Repository in this folder.
 - In the header of the html page where to incorporate the Swagger documentation import the following CSS and javascript files:
{% highlight html %}
<head>
         .....
  	<link href='./swagger-ui/css/typography.css' media='screen' rel='stylesheet' type='text/css'/>
  	<link href='./swagger-ui/css/reset.css' media='screen' rel='stylesheet' type='text/css'/>
  	<link href='./swagger-ui/css/screen.css' media='screen' rel='stylesheet' type='text/css'/>
  	<link href='./swagger-ui/css/reset.css' media='print' rel='stylesheet' type='text/css'/>
  	<link href='./swagger-ui/css/print.css' media='print' rel='stylesheet' type='text/css'/>

  	<script src='./swagger-ui/lib/object-assign-pollyfill.js' type='text/javascript'></script>
  	<script src='./swagger-ui/lib/jquery-1.8.0.min.js' type='text/javascript'></script>
  	<script src='./swagger-ui/lib/jquery.slideto.min.js' type='text/javascript'></script>
  	<script src='./swagger-ui/lib/jquery.wiggle.min.js' type='text/javascript'></script>
  	<script src='./swagger-ui/lib/jquery.ba-bbq.min.js' type='text/javascript'></script>
  	<script src='./swagger-ui/lib/handlebars-4.0.5.js' type='text/javascript'></script>
  	<script src='./swagger-ui/lib/lodash.min.js' type='text/javascript'></script>
  	<script src='./swagger-ui/lib/backbone-min.js' type='text/javascript'></script>
  	<script src='./swagger-ui/swagger-ui.min.js' type='text/javascript'></script>
  	<script src='./swagger-ui/lib/highlight.9.1.0.pack.js' type='text/javascript'></script>
  	<script src='./swagger-ui/lib/highlight.9.1.0.pack_extended.js' type='text/javascript'></script>
  	<script src='./swagger-ui/lib/jsoneditor.min.js' type='text/javascript'></script>
  	<script src='./swagger-ui/lib/marked.js' type='text/javascript'></script>
  	<script src='./swagger-ui/lib/swagger-oauth.js' type='text/javascript'></script>
 </head>
   .....
{% endhighlight %} 
 - In the body of the same html page it is necessary to place a div where the Swagger documentation will be placed and then call the Swagger specific function to load the relevant API documentation 
{% highlight html %}
 <body>
	.....
	
	<div id="swagger-ui-container"></div>
	
	<script type="text/javascript">
	
		jQuery(function () {
			hljs.configure({
				highlightSizeThreshold: 5000
			});

			// Pre load translate...
			if(window.SwaggerTranslator) {
				window.SwaggerTranslator.translate();
			}
	  
			window.swaggerUi = new SwaggerUi({
				url: "https://www.ebi.ac.uk/europepmc/annotations_api/v2/api-docs.json",
				dom_id: "swagger-ui-container",
				supportedSubmitMethods: ['get'],
				docExpansion: "list",
				jsonEditor: false,
				defaultModelRendering: 'example',
				showRequestHeaders: false,
				showOperationIds: false,
				validatorUrl:null
			});

			window.swaggerUi.load();
		});
	</script>  
	
	...
</body>
{% endhighlight %} 

The javascript object SwaggerUi will load the API documentation described through the url property and will place it inside the dom identified by the dom_id property value.
Below are details of the properties that can be set to the SwaggerUi object:

<table>
<thead>
<tr>
<th>Parameter Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>url</td>
<td>The url pointing to <code>swagger.json</code> (Swagger 2.0) or the resource listing (earlier versions) as per <a href="https://github.com/OAI/OpenAPI-Specification/">OpenAPI Spec</a>.</td>
</tr>
<tr>
<td>authorizations</td>
<td>An authorization object to be passed to swagger-js.  Setting it here will trigger inclusion of any authorization or custom signing logic when fetching the swagger description file.  Note the object structure should be <code>{ key: AuthorizationObject }</code></td>
</tr>
<tr>
<td>spec</td>
<td>A JSON object describing the OpenAPI Specification. When used, the <code>url</code> parameter will not be parsed. This is useful for testing manually-generated specifications without hosting them. Works for Swagger 2.0 specs only.</td>
</tr>
<tr>
<td>validatorUrl</td>
<td>By default, Swagger-UI attempts to validate specs against swagger.io's online validator. You can use this parameter to set a different validator URL, for example for locally deployed validators (<a href="https://github.com/swagger-api/validator-badge">Validator Badge</a>). Setting it to <code>null</code> will disable validation. This parameter is relevant for Swagger 2.0 specs only.</td>
</tr>
<tr>
<td>dom_id</td>
<td>The id of a dom element inside which SwaggerUi will put the user interface for swagger.</td>
</tr>
<tr>
<td>booleanValues</td>
<td>SwaggerUI renders boolean data types as a dropdown. By default it provides a 'true' and 'false' string as the possible choices. You can use this parameter to change the values in dropdown to be something else, for example 0 and 1 by setting booleanValues to new Array(0, 1).</td>
</tr>
<tr>
<td>docExpansion</td>
<td>Controls how the API listing is displayed. It can be set to 'none' (default), 'list' (shows operations for each resource), or 'full' (fully expanded: shows operations and their details).</td>
</tr>
<tr>
<td>apisSorter</td>
<td>Apply a sort to the API/tags list. It can be 'alpha' (sort by name) or a function (see Array.prototype.sort() to know how sort function works). Default is the order returned by the server unchanged.</td>
</tr>
<tr>
<td>operationsSorter</td>
<td>Apply a sort to the operation list of each API. It can be 'alpha' (sort by paths alphanumerically), 'method' (sort by HTTP method) or a function (see Array.prototype.sort() to know how sort function works). Default is the order returned by the server unchanged.</td>
</tr>
<tr>
<td>defaultModelRendering</td>
<td>Controls how models are shown when the API is first rendered. (The user can always switch the rendering for a given model by clicking the 'Model' and 'Model Schema' links.) It can be set to 'model' or 'schema', and the default is 'schema'.</td>
</tr>
<tr>
<td>onComplete</td>
<td>This is a callback function parameter which can be passed to be notified of when SwaggerUI has completed rendering successfully.</td>
</tr>
<tr>
<td>onFailure</td>
<td>This is a callback function parameter which can be passed to be notified of when SwaggerUI encountered a failure was unable to render.</td>
</tr>
<tr>
<td>highlightSizeThreshold</td>
<td>Any size response below this threshold will be highlighted syntactically, attempting to highlight large responses can lead to browser hangs, not including a threshold will default to highlight all returned responses.</td>
</tr>
<tr>
<td>supportedSubmitMethods</td>
<td>An array of of the HTTP operations that will have the 'Try it out!' option. An empty array disables all operations. This does not filter the operations from the display.</td>
</tr>
<tr>
<td>oauth2RedirectUrl</td>
<td>OAuth redirect URL</td>
</tr>
<tr>
<td>showRequestHeaders</td>
<td>Whether or not to show the headers that were sent when making a request via the 'Try it out!' option. Defaults to <code>false</code>.</td>
</tr>
<tr>
<td>jsonEditor</td>
<td>Enables a graphical view for editing complex bodies.  Defaults to <code>false</code>.</td>
</tr>
</tbody>
</table>	
 - Now it is possible to customize the standard style of the Swagger documentation tweaking both the default Swagger css and the site application css as required. 
	An example of the result can be found at [Europe PMC Annotations API documentation page][5]


  [1]: https://swagger.io/
  [2]: https://www.ebi.ac.uk/europepmc/annotations_api/swagger-ui.html
  [3]: https://www.ebi.ac.uk/europepmc/annotations_api/v2/api-docs.json
  [4]: https://github.com/swagger-api/swagger-ui/tree/2.x/dist
  [5]: http://europepmc.org/AnnotationsApi