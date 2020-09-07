
# User inactivity report based on lastLogin


# Overview

To improve the security and also to minimize the license usage in a Okta org. Customers want to send a notification or Suspend or deactivate users in an Okta org if the user is not logged in for x number of days.

This flow by default adds the user to a group in Okta if the user is not logged in for x number of days. You can change the logic based on your requirement.

This flow also handles rate limiting. This flow is triggered with a scheduled job everyday. Which runs between a specific time, Check the screenshot below. I have my job starts at 5 PM and ends 6 PM PST. It starts every 5 mins. 



<p id="gdcalert1" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image1.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert2">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image1.png "image_tooltip")


This flow is built with rate limiting support. Okta returns 200 users per page. This flow will process 49 pages and store the 50 th page information in the table. When the flow is restarted in 5 mins, It will start processing from the 50th page.

Below are some of the run time statistics based on the users in an org. These times will change frequently based on the time of execution and other factors. Okta also consistently improves our infrastructure to process these jobs in more efficient ways. Please test the flows run time in your org and update the scheduler accordingly.



<p id="gdcalert2" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image2.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert3">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image2.png "image_tooltip")



### 
**Before you get Started / Prerequisites**

Before you get started, you will need:



*   Access to an Okta tenant with Okta Workflows enabled for your org
*   Setup a group in Okta for lastLoginreport.

### 
**Setup Steps**

*   Open the Schedule-Trigger-01 and click on the time icon in the first card to alter your schedule.

    

<p id="gdcalert3" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image3.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert4">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image3.png "image_tooltip")


*   Update the Okta connections in 03 and 04 flows. Flow numbers can be found at the end of each flow. This is the order the flow executes.
*   Open the “process all users” flow and update the days you want to go back for validating the last Login. If you want to validate users that are not logged in for 10 days. Then enter 10. By default the value is set as 30 days.



<p id="gdcalert4" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image4.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert5">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image4.png "image_tooltip")




*   Go to Okta and click on the group you created. Copy the groupID at the end of the URL.



<p id="gdcalert5" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image5.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert6">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image5.png "image_tooltip")




*   Open the “LastLoginValidation-04” flow and update the groupID in the Add user to group card.

### 
**Testing this Flow**

*   Test the flow manually. If everything worked well, It should add the lastLoginnextRow,time in the table. 
*   Open the NextRow table from the tables section.



<p id="gdcalert6" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image6.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert7">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image6.png "image_tooltip")




*   Check the flow history tab for errors and troubleshooting.
