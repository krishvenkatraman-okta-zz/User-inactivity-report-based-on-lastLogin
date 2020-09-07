
# User inactivity report based on lastLogin


# Overview

To improve the security and also to minimize the license usage in a Okta org. Customers want to send a notification or Suspend or deactivate users in an Okta org if the user is not logged in for x number of days.

This flow by default adds the user to a group in Okta if the user is not logged in for x number of days. You can change the logic based on your requirement.

This flow also handles rate limiting. This flow is triggered with a scheduled job everyday. Which runs between a specific time, Check the screenshot below. I have my job starts at 5 PM and ends 6 PM PST. It starts every 5 mins. 

![image](https://user-images.githubusercontent.com/14205843/92412898-8dd50d00-f102-11ea-9d49-16d46f9bf2be.png)


This flow is built with rate limiting support. Okta returns 200 users per page. This flow will process 49 pages and store the 50 th page information in the table. When the flow is restarted in 5 mins, It will start processing from the 50th page.

Below are some of the run time statistics based on the users in an org. These times will change frequently based on the time of execution and other factors. Okta also consistently improves our infrastructure to process these jobs in more efficient ways. Please test the flows run time in your org and update the scheduler accordingly.

![image](https://user-images.githubusercontent.com/14205843/92412923-af35f900-f102-11ea-84bc-8372b4061edc.png)


### 
**Before you get Started / Prerequisites**

Before you get started, you will need:



*   Access to an Okta tenant with Okta Workflows enabled for your org
*   Setup a group in Okta for lastLoginreport.

### 
**Setup Steps**

*   Open the Schedule-Trigger-01 and click on the time icon in the first card to alter your schedule.

![image](https://user-images.githubusercontent.com/14205843/92412967-db517a00-f102-11ea-98f7-be7b7be37f51.png)


*   Update the Okta connections in 03 and 04 flows. Flow numbers can be found at the end of each flow. This is the order the flow executes.
*   Open the “process all users” flow and update the days you want to go back for validating the last Login. If you want to validate users that are not logged in for 10 days. Then enter 10. By default the value is set as 30 days.

![image](https://user-images.githubusercontent.com/14205843/92413011-089e2800-f103-11ea-996b-229fe1be521f.png)


*   Go to Okta and click on the group you created. Copy the groupID at the end of the URL.

![image](https://user-images.githubusercontent.com/14205843/92413044-2a97aa80-f103-11ea-93f2-4366865d1aa5.png)

*   Open the “LastLoginValidation-04” flow and update the groupID in the Add user to group card.

### 
**Testing this Flow**

*   Test the flow manually. If everything worked well, It should add the lastLoginnextRow,time in the table. 
*   Open the NextRow table from the tables section.

![image](https://user-images.githubusercontent.com/14205843/92413091-54e96800-f103-11ea-8604-7ba40a43afda.png)

*   Check the flow history tab for errors and troubleshooting.
