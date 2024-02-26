# Incident Flow Steps
A collection of 6 custom flow steps for working with xMatters Incidents in xMatters Flow Designer. 

The steps come packaged in a workflow with a tester form called *Run Flow Step*. You can try out each step by filling in the appropriate form section in a messaging form then view the output either directly in the flow's activity log or in an alert notification.

---------
<kbd>
  <a href="https://support.xmatters.com/hc/en-us/community/topics"><img src="https://github.com/xmatters/xMatters-Labs/raw/master/media/disclaimer.png"></a>
</kbd>

----------

# Pre-Requisites
* Access to an xMatters instance with admin rights, e.g. Full Access User, Developer and/or Company Supervisor roles. 
* If you don't have an xMatters instance, [try one for free](https://www.xmatters.com/free)!

# Files
* [xMattersIncidentFlowSteps.zip](xMattersIncidentFlowSteps.zip) - an xMatters workflow zip containing 2 forms, 1 flow canvas and 6 custom flow steps. Do not inflate the zip file. See Installation instructions below.

# Incident Flow Steps
The new flow steps are...
*	**xM Get Incident With Properties** 

	<kbd>  <img src="/media/xmGetIncWithProps.png" width="250"> </kbd>
	
An enhanced version of the built-in Get Incident step. It outputs all the usual details of an xMatters Incident *plus custom Incident properties* and Incident Type, e.g. Application, Site, Platform, Region, Business Impact Asessment. 

N.B. YOU MUST ADD AN OUTPUT FOR EACH NAMED PROPERTY. AND OF COURSE, THE INCIDENT NEEDS TO HAVE THE PROPERTIES! For example, suppose you have defined an Incident Type called Scary Incident, and this Incident Type has custom properties called Incident Level, Region and Company. 

<img src="/media/scaryIncident.png" width="900">

Update the step configuration and add outputs called Scary Incident, Region and Company. 

<img src="/media/defineOutputs.png" width="500">
	
Provided the Incident properties exist, you will see them in the output, in addition to all the regular Get Incident outputs.

<img src="/media/stepOutputs.png" width="250">

However, if you don't want to do this, we have your back. You also get an output called propertiesObject which bundles all Incident properties into an object of key-value pairs. This is easy to parse in a subsequent flow step.

<img src="/media/propertiesObject.png" width="500">

P.S. Learn about Incident Types in xMatters [here](https://help.xmatters.com/ondemand/incidentmgmt/incident-types.htm)

*	**xM Search Incidents**

	<kbd>  <img src="/media/xmSearchIncidents.png" width="250"> </kbd>
	
Find one or more xMatters Incidents. A comprehensive step that lets you search by many different properties. The list includes Status (e.g In Progress), Severity (e.g. Critical), Incident ID, Summary, Description, Incident Type, Impacted Services, and custom property key/value pairs.

 As you move down the options, they are AND'd together. We encourage you to read the API notes for [xMAPI Get Incidents](https://help.xmatters.com/xmapi/index.html#incidents) to understand the various options. N.B. After the API returns data, the step filters the returned data from xMAPI to further check for Incident Type and Incident Property key/value pairs. The step returns a list of Incident IDs and a count


*	**xM Write Structured Work Note**

	<kbd>  <img src="/media/xmWriteStructuredWorkNote.png" width="250"> </kbd>

Adds a structured timeline note to an xMatters incident matching the key, e.g.  *weather: rainy*. The step avoids repetition, and will not enter a note if it matches the last note entered. This is to avoid the same work note appearing over and over again, e.g. *weather: rainy* followed soon after by another *weather: rainy*. A structured work note is great for storing data, e.g. links to external IDs, in a way that cannot be overwritten by a user via the UI. 

*	**xM Get Structured Work Note**

	<kbd>  <img src="/media/xmGetStructuredWorkNote.png" width="250"> </kbd>

After writing a structured work note, you'll probably want to get it. 

*	**xM Remove Service from Incident**

	<kbd>  <img src="/media/xmRemoveServiceFromIncident.png" width="250"> </kbd>

Clears all Services from an xMatters Incident record. This is not possible via the built-in Update Incident step, in which an empty imput for Impacted Services results in no update to the Service.

*	**xM Get Incident URL**

	<kbd>  <img src="/media/xmGetIncidentURL.png" width="250"> </kbd>

Returns a URL to link directly to an xMatters Incident. Useful for including in Alerts, so resolvers can quickly find their way to the Incident console. 



# Installation
1. Log into xMatters as a user with either the Developer or Full Access User role. Navigate to Workflows, click the Import button on the top right and import the  [xMattersIncidentFlowSteps.zip](xMattersIncidentFlowSteps.zip) file. This is what you will see in the list of workflows.
	<kbd>  <img src="/media/incident_flow_steps.png" width="900"> </kbd>
	
2. Navigate into the new workflow. You will see a list of two forms. Set Sender Permissions on the upper form, Run Flow Step. To do this, click the left most button. Ensure the form is accessible by selecting <b>Web UI</b><br>
  <img src="/media/web_ui.png" width="350"> 

 and then <b>Sender Permissions</b>. Add users or roles who can access the form. We recommend allowing all those with _Full Access User_ and _Developer_ roles to use the form. <br>
 <img src="/media/sender_permissions.png" width="350"> 

The lower form, **Results**, is triggered by the upper form. To deploy it, choose _Enable For Web Service_.
	
3. OPTIONAL. By default, only the user who imports the workflow has permission to use and modify the custom steps within the workflow. We recommend broadening permissions to allow all those with the Developer role to use and/or edit your new flow steps. To do this, highlight the FLOW DESIGNER tab to the right of FORMS. Open the Run Flow Step flow canvas. 
	<kbd>  <img src="/media/run_flow_step_canvas.png" width="900"> </kbd>
	
4. To the right of the screen on the Palette, highlight the CUSTOM tab. Navigate to each new flow step in turn. Click the gear icon then <b>Usage Permissions</b>. In the pop-up window, grant ACCESS to other users/roles as required, e.g. select the Developer role and grant permission to Edit Step.

	<kbd>  <img src="/media/step_usage_permissions.png" width="500"> </kbd>


	<kbd>  <img src="/media/developer_usage.png" width="500"> </kbd>
	
# Testing
You can try out each new custom step via the **Run Flow Step** messaging form.   Navigate to Messaging > xMatters Incident Flow Steps > Run Flow Step. 

<kbd>  <img src="/media/messaging.png" width="900"> </kbd>

Choose which step to run in the first dropdown.  Each step has it’s own corresponding form section with some demo values in it. You can use the demo values supplied or over-type with your own test values. 

<kbd>  <img src="/media/run_flow_step_form.png" width="500"> </kbd>
	
OPTIONAL: At the bottom of the form, if you want, you can set yourself as a Recipient. When you click Send Message, you will get an initial email notification confirming the flow has been started. A short while later, a second email will arrive with the step’s output values clearly shown. Alternatively, you can view the output either in the Alert Report

<kbd>  <img src="/media/alerts_report.png" width="900"> </kbd>

Or in the Activity Log of the Run Flow Step canvas.


<kbd>  <img src="/media/activity_log.png" width="900"> </kbd>

# Troubleshooting
Navigate to xMatters Incident Flow Steps > Flow Designer tab > Run Flow Step canvas. You can see how the correct step is selected based on an initial Switch block. Each custom step outputs log notes. If a step fails, you can open the **Activity Log** and inspect the log messages.



You are also able to view the source of each step by opening it from the CUSTOM steps palette and selecting the step's SCRIPT tab. As with all xMatters custom steps, the scripting language is JavaScript running in the xMatters cloud environment rather than on the browser.
