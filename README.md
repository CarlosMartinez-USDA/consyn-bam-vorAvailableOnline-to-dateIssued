# Elsevier CONSYN XSLT
Updates
-  [bam:elements](#bamelements)
	- [latest](#latest)


### bam\:elements

Elsevier provided notice of two newly deployed date elements on December 14, 2022. The new dates present opportunity to better capture dateIssued element and relatedItem/part/text[@type] subelements more accurately.  


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

- \<url\> was given an @displayLabel attribute, stating "Available on the publisher's site."

- bam:articleNumebring detail type attribute changed from "article" to "issue" to accoodate auto-generation of citations via Primo VE.
 
### Latest
|_fileChanged_|_dateChanged_|_Example/Explanation_|
|--|--|--|
|_notice_ |2022-12-14 | Elsevier CONSYN deploys 2 new date elements
| consyn-to-mods.xsl |2023-01-26| bam date elements added 
|  [**consyn-to-mods.xsl**]() | 2023-04-19  | updated order of preferred dates selected in order to align dateIssued with relatedItem/part/text[@type] date elements. 
| | |

 
* dateIssued and relatedItem selected from source XML elements in the following order:
 	- prism:coverDisplayDate
 	- prism:coverDate
	- bam:vorAvailableOnline
 	- bam: availableOnline
	- ce:date-ccepted
 	- ce:copyright
 
