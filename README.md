
# User inactivity report based on lastLogin


# Overview

To improve the security and also to minimize the license usage in a Okta org. Customers want to send a notification or Suspend or deactivate users in an Okta org if the user is not logged in for x number of days.

This flow by default adds the user to a workflow table, If the user is not logged in for 30 number of days. You can change the logic based on your requirement. Logic is in 0.1.4 flow. This flow is designed to run for active users in the org.

This flow handles rate limiting, pagination. Flow is triggered with a scheduled job everyday between specific time, Check the screenshot below. I have my job scheduled to run at 8 PM PST. You can change this based on your requirement.

![image](https://user-images.githubusercontent.com/14205843/94765551-0c1e7b00-0360-11eb-9a3f-f4779b3b41c0.png)

This flow needs to be configured to run repeteadly for x number of times based on the number of Active users in the Org.  

This flow is tested with below run times.

100000 users can be processed at 2 Hours. You should use this flow only if your org has less than 200,000 users. Anything more will take more execution time. Also execution times varies based on the time of execution and tenants.


### 
**Before you get Started / Prerequisites**

Before you get started, you will need:


*   Access to an Okta tenant with Okta Workflows enabled for your org
*   Find the number of Active users in the Okta instance under Directory - People

### 
**Setup Steps**

*   Open the 0. master_flow and click on the time icon in the first card to alter your schedule.

![image](https://user-images.githubusercontent.com/14205843/94767369-04aba180-0361-11eb-839d-249be2882e1f.png)

*   Open the 0. master_flow and update the number of days you want to go back for validate the lastLogin. I use current date - 30 days.

![image](https://user-images.githubusercontent.com/14205843/94767497-5fdd9400-0361-11eb-82b8-9346200462bc.png)

*   Now update the Count in the last card. This count is created based on number of active users in the org. Okta will process 200 users per page. So if you have 100000 Active users. You can divide 100000/200. 500 pages has to be processed. So update the count based on your org active user count. This can be set to a lower number like as low as 1, So to test you can just process one single 200 users batch.

![image](https://user-images.githubusercontent.com/14205843/94767605-b519a580-0361-11eb-9fa8-808905abe163.png)

*   Open the 0.1 flow and update the Okta org connection

![image](https://user-images.githubusercontent.com/14205843/92413011-089e2800-f103-11ea-996b-229fe1be521f.png)


*   Open the 0.1.4 flow if you want to change logic for the user that matches the condition. For example if you want to add them to a Okta group or send a email, You can add that here.


### 
**Testing this Flow**

*   Test the flow manually. If everything worked well, you should be able to see the inactivityReport table updated with users.

![image](https://user-images.githubusercontent.com/14205843/94768438-4f7ae880-0364-11eb-9e18-5a3e1f03fb55.png)

*   Check the flow history tab for errors and troubleshooting.
