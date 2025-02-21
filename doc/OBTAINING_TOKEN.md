# Half manual Login Flow
### This method does require some manual steps, **including the usage of the developer tools!** of your browser

> [!WARNING]
> Although this have been tested multiple times (in January 2025), It can't be guaranteed the method will last as Ford are consistently making changes!

> [!NOTE]
> This process requires the [1.71 release (or higher)](https://github.com/marq24/ha-fordpass/releases/tag/1.71-Release) of the fordpass integration 


### **Step I:**
1. In Home Assistant: Enter your Fordpass username
2. You can select an alternative Region, but currently I do not expect that any other region then `USA` will work.

![image](./../images/001.png)


### **Step II:**
1. Copy the URL that has been generated and paste it in your additional browser. 

> [!IMPORTANT]
> Ensure you have enabled the Developer tools before pressing "log in" as you will be required to capture a header once logged in!  
[:link: Chromium based dev tools helper (Chrome / Edge)](./DEV-TOOLS.md)  
[:link: Firefox dev tools helper](./DEV-TOOLS.md#firefox)

![image](./../images/002.png)

2. In your second browser (where you pasted the URL), the Ford Login dialog should be display. 

3. Enter your FordPass credentials and click `Log in`.
> [!NOTE]
> After you have pressed the login button, the Ford Login website will just show a spinner and will not continue to load - this is the intended behavior! At this point you are able to obtain the code by using the browser tools (see next step 4).

4. Now you must use the browser tools and select the `Network tab` of the web console and view the headers section.
   
   - The last request (probably already showed in red) is the one we are interested in... Since this last request contains the code we must capture for the integration it should start with `userauthorized/...`
   - You are looking for the contents of the "Location Header" as shown in the pic below
   - The output should look similar to the following string, starting with `fordapp://`:
   - ```fordapp://userauthorized/?code=eyJraWQiOiItSm9pdi1OX1ktUWNsa***************************```
   - **Ensure you capture the entire string (copy the raw output and not the wrapped text)** and enter it into the text box of the home assitant setup dialog.
   - You then can close the Ford login browser window 

> [!NOTE]
> Again - the Ford login website will not **fully loaded**. The login page will just continue to spin. 

![webrequst](./../images/003.png)


### **Step III:** 
- Once you've entered the copied token back in the home assistant integration setup dialog the integration should go off and get you a new set of tokens and then ask what vehicles you want to add.