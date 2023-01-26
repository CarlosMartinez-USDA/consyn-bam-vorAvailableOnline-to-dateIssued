# Elsevier CONSYN XSLT
## Contents

 - [Issues](#issues)
 - [Updates](#updates)
 - [OtherUpdates](#otherupdates)
 

### Issues

bam:vorAvailableOnline-to-dateIssued
 Using newly added Consyn elements bam:vorAvailableOnline as priority result for mods:originInfo/dateIssued


### Updates
 -  Two new metadata fields related to publication dates:

	1.  **_bam:availableOnline_**: The first date on which any version of the resource has been published on any of Elsevier's platform.
	2.  **_bam: vorAvailableOnline_**: The date upon which the first final version of the resource is published on any of Elsevier's online platforms.


#### The decision to use bam:vorAvailableOnline as the first choice for \<dateIssued\> was made.
#### Sample of the updated XML: 
```xml
   <dp:availableOnlineInformation>
      <bam:availableOnline xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">2022-03-30T00:00:00.000Z</bam:availableOnline>
      <bam:vorAvailableOnline xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">2022-03-30T00:00:00.000Z</bam:vorAvailableOnline>
   </dp:availableOnlineInformation> 
```
#### Template used to capture \<dateIssued\> metadata: 
```xml
        <xsl:template match="bam:vorAvailableOnline" mode="origin">
            <!--one-->
            <dateIssued encoding="w3cdtf" keyDate="yes">
                <xsl:value-of select="substring-before(., 'T')"/>
            </dateIssued>
        </xsl:template>
```
##### *Using _fn:substring-before(  )_ to capture just the date portion of the field, builds _w3cdtf_ formatted dates. 

####  OtherUpdates
- \<url\> was given an @displayLabel attribute, stating "Availabe on the publisher's site."

- bam:articleNumebring detail type attribute changed from "article" to "issue" to accoodate auto-generation of citations via Primo VE.
 