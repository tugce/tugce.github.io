---
layout: post
title:  "Salesforce MDAPI Deployment Errors (1) - In Field: name - no WorkflowFieldUpdate named X found (EntitlementProcess)"
date:   2020-08-15 10:00:00
categories: salesforce metadata-api mdapi deployment
---

During deployment of an Entitlement Process we've run into a weird issue. <b>In Field: name - no WorkflowFieldUpdate named X found.</b> Issue was weird because field update and field <b>did</b> existed and necessary permissions were given. So what is the problem? Let's review the sample metadata file for the EntitlementProcess.

I've created a sample EntitlementProcess and retrieved it with below package.xml
~~~ xml
  <?xml version="1.0" encoding="UTF-8"?>
  <Package xmlns="http://soap.sforce.com/2006/04/metadata">
     <types>
          <members>ts test ep</members>
          <members>ts test ep_v2</members>
          <name>EntitlementProcess</name>
      </types>
      <version>48.0</version>
  </Package>
~~~
Resulting metadata file is below. Notice that in the Success Actions name is just Thread_Id. When I deployed the package back everything is fine.

~~~ xml
<?xml version="1.0" encoding="UTF-8"?>
<EntitlementProcess xmlns="http://soap.sforce.com/2006/04/metadata">
    <SObjectType>Case</SObjectType>
    <active>true</active>
    <description>Test for blog</description>
    <entryStartDateField>Case.CreatedDate</entryStartDateField>
    <exitCriteriaFilterItems>
        <field>Case.IsClosed</field>
        <operation>equals</operation>
        <value>true</value>
    </exitCriteriaFilterItems>
    <exitCriteriaFilterItems>
        <field>Case.Origin</field>
        <operation>equals</operation>
        <value>Phone</value>
    </exitCriteriaFilterItems>
    <isVersionDefault>true</isVersionDefault>
    <milestones>
        <milestoneCriteriaFilterItems>
            <field>Case.Status</field>
            <operation>equals</operation>
            <value>Working</value>
        </milestoneCriteriaFilterItems>
        <milestoneName>TS - First Milestone</milestoneName>
        <minutesToComplete>180</minutesToComplete>
        <successActions>
            <name>Thread_Id</name>
            <type>FieldUpdate</type>
        </successActions>
        <useCriteriaStartTime>false</useCriteriaStartTime>
    </milestones>
    <name>TS Test EP</name>
    <versionMaster>5520J0000004PGM</versionMaster>
    <versionNumber>2</versionNumber>
</EntitlementProcess>
~~~
However if you retrieve the EntitlementProcess with the WorkflowFieldUpdate it is referencing, the metadata file is retrieved as below.

~~~ xml
<successActions>
    <name>Case.Thread_Id</name>
    <type>FieldUpdate</type>
</successActions>
~~~

Notice how name changed from <b>Thread_Id</b> to <i>Case.Thread_Id</i>

And if we try to deploy this package we have the error from the title: <b>In field: name - no WorkflowFieldUpdate named Case.Case.Thread_Id found</b>

I've noticed that Case.Case... was not looking right and after checking the <a href="https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_entitlementprocess.htm">sample metadata file</a> from Salesforce documentation I've noticed extra sobject name in front of the WorkflowFieldUpdate.

This issue is not documented anywhere except <a href="https://trailblazer.salesforce.com/issues_view?id=a1p30000000T0oHAAS&title=deployments-of-approval-process-with-workflow-field-updates-throw-error-stating-that-the-workflow-field-update-doesn-t-exist-for-that-sobject">a similar old known issue</a> that was fixed in Spring 14.

<b>Workaround</b>

Workaround to this issue is either <b>deploying WorkflowFieldUpdate separately</b> or <b>changing the file manually by removing the object name in actions part</b> and then deploying that way.

<div id="disqus_thread"></div>
<script>
    /**
     *  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
     *  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables
     */
    /*
    var disqus_config = function () {
        this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
        this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
    };
    */
    (function() {  // DON'T EDIT BELOW THIS LINE
        var d = document, s = d.createElement('script');

        s.src = '//ztugcesirincom.disqus.com/embed.js';

        s.setAttribute('data-timestamp', +new Date());
        (d.head || d.body).appendChild(s);
    })();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript" rel="nofollow">comments powered by Disqus.</a></noscript>
