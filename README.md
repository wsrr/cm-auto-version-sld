# cm-auto-version-sld

Sample code for IBM(R) WebSphere(R) Service Registry and Repository (WSRR) showing how you can automate the creation of a version and service level definition (SLD) when a business service is approved.

This uses the Configurable Modifier feature of WSRR. The Configurable Modifier is an XML driven modifier, which can change content in WSRR in reaction to things happening, such as creation, update, delete, transition of objects in WSRR.

## Details

The code is in two parts. 

### GenerateSV.xml

The configurable modifier action file GenerateSV.xml creates an SLD and sets the name based upon the business service name. 

The action also creates a service version. The name is the same as the business service, the description appropriate and the version set to "1.0.0". The owning organization is set to that of the business service by finding the owning organization of the business service. The relationship that has an SLD is set to point to the SLD created in the first create-action.

The action finally updates the business service to point to the version which was created.

### Triggers.xml

This trigger file contains the XML fragment needed to make the action run when the business service is approved. Therefore the trigger element should be taken and pasted into your current Triggers.xml, so that the rule is added to the existing rules.

The trigger rule means that when a business service is pushed through the approve charter transition, so it is approved, the action in GenerateSV.xml is run and a new version and SLD are created.

## Configuration

To use the configurable modifier action you need to:

1. Add the `GenerateSV.xml` file into your WSRR profile as a Configurable Modifier configuration. The name of the configuration is not important. Use either WSRR Studio or the WSRR Web UI to add the file. See the WSRR Knowledge Center page [Loading an actions file](http://www.ibm.com/support/knowledgecenter/SSWLGF_8.5.5/com.ibm.sr.doc/twsr_config_mod_load_actions_file.html).

2. Modify the existing WSRR triggers file to add the content from Triggers.xml. Use either WSRR Studio or the WSRR Web UI. Copy the `trigger` element content and paste it into the existing WSRR triggers file at the same level as other `trigger` elements. See the WSRR Knowledge Center page [Modifying a triggers or actions file by using the web UI](http://www.ibm.com/support/knowledgecenter/SSWLGF_8.5.5/com.ibm.sr.doc/twsr_config_mod_file_modify.html) for more details.

3. When using WSRR Studio, generate your profile project, then publish it to your WSRR server and activate the profile. You can also generate and then synchronize with the active profile on your WSRR server and publish the changed configurations.

## Testing

To test you need to:

1. Create a business service in the WSRR UI.
2. Transition the business service to the Approved state.
3. Examine the details of the business service.

A version and SLD will have been created and can be seen from the details of the business service.

## License

Licensed under the Apache License, Version 2.0 (the "License"). See license.txt.
