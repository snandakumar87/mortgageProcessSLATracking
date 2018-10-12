
SLA Due Date Tracking

Prerequisites: Import the mortgage process sample.
Setting the SLA Due Date for a Process/Task:
SLA Due date can be assigned to a process by providing a due date property from the property pane as below.


In this example we have set a process level sla due date of 2s. Once the 2s is elapsed, SLA is Violated on the process instance, and the event can be caught and handled.
The instance shows that the SLA compliance is violated, and custom reports can be created on the SLA properties.

Now let us catch the SLA violation event and send an email notification. 
Create a custom Process Event listener to handle the SLA violation.
	We create a class that implements the ProcessEventListener. SLA tracking can be performed using the methods, beforeSLAViolated and afterSLAViolated.

We override the 
afterSLAViolated(), and create a process instance to handle the escalation flow. The listener can be created as a standalone maven project which can then be imported into business central.
https://github.com/snandakumar87/slatracking/tree/master/process-event-listener


2)Let us create a escalation handling process under the mortgage project, where we have a simple email task to handle the escalation flow.
Configure the email params,

Once the handling process has been created, we now have to register the EmailWorkItemHandler and register the listener we created to the mortgage project in business central.

Make sure to add the From and To email address on the Email Service Task and ensure Email Config is done. Refer to http://planet.jboss.org/post/email_configuration_for_jbpm

3) Open up the settings tab -> Artifcats
Upload the jar file of the custom listener which we had created in step1. 
Open up the mortgage project -> Settings -> Dependencies -> Add from repository

Choose the event listener maven artifact and import the dependency.
Next navigate to settings tab -> Artifcats -> Deployments -> Event Listener and add the constructor of the custom event listener we had created.

Next for sending the email notification, we have to create an email workitemhandler.

Once all the configuration is done, deploy the process. When the instance is started, and after 2s have elapsed, you can see that email has been sent. Please refer to https://docs.google.com/document/d/1QrFPLEm-cW-oeM0B7sqNF361m9aLue8pzHkxCAcNLeI/edit?usp=sharing

Similarly any custom logic can be implemented to handle the SLA violation.

