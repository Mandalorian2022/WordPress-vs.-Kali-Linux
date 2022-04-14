# Assignemnt 7&8 - WordPress VS Kali Linux

Time Spent: 12 hours

> This Penetration testing has been done on my local wordpress server vs kali linux (Debian 9). This Assignment was done for educational purposes only :warning:

The first step for me was to make sure I have a correct and stable version of docker and docker-compose. 
![dockerup2](https://user-images.githubusercontent.com/96266650/163241149-041097a9-18ef-409d-9ce5-7f6ae7fc9c81.png)


## WPScan
I found 3 active Vulnurbulities with the following plugins installed:
- [x] contact-form-7
  -  Version: 5.3 

- [x]  reflex-gallery
  -  Version: 3.1.3


![ezgif com-gif-maker (1)](https://user-images.githubusercontent.com/96266650/163244444-b5fd6df0-df3f-447d-bbc8-78c2c1c29856.gif)
  > It was interesting to see how the communication between wpscan and my wordpress server was captured in my server log. 

## EXPLOITS

1- Contact Form 7 < 5.3.2 - Unrestricted File Upload
  This vulnerability allows the attacker to create and upload a file with filename containing double-extensions, sperated by a non-printable or special characters.
  
  - Proof Of Concept:
  This plugin doesn't check for empty spaces therefore even if the required attachment file is .png or .jpg, we can simply add an extra extention to our exploit.php      file. 

![exploit1](https://user-images.githubusercontent.com/96266650/163256254-35bbdc15-b604-4423-93d9-1ec3b97de7cf.png)
![exploit1-2](https://user-images.githubusercontent.com/96266650/163257041-c8ee9688-ef15-4f40-a34f-f67c75f9e399.gif)




2- Reflex Gallery <= 3.1.3 - Arbitrary File Upload
  This vulnerability was exploited by msfconsole by searching for specific exploit in the database. 
![Exploit2](https://user-images.githubusercontent.com/96266650/163274154-47a1fa3b-e536-442f-ba85-a64ab71421a7.png)
Simple `ls` command now shows all the pictures that I uploaded along with other folders on my wordpress server.

![exploit2-2](https://user-images.githubusercontent.com/96266650/163285943-9dd4a077-9689-43fa-b061-8bc34691a80a.gif)
![image](https://user-images.githubusercontent.com/96266650/163293892-efbc5e8b-3046-4746-a8a2-1c87773fea6f.png)


Now that we have access to the files. we can also delete them by using `rm`.

![image](https://user-images.githubusercontent.com/96266650/163286812-6bf9046b-90ea-4a8d-b714-4d4985af71b5.png)


3- Reflex Gallery - jQuery prettyPhoto DOM Cross-Site Scripting (XSS)
Since I knew I already have an open access to uploading and deleting material and folders from meterpreter command line. I used some basic vim command to edit and 
deploy more malicious commands. I edited the new user folder and adding a xss command and adding new users to list. and ultimatly by doing this I can edit any folder and delete or add more XSS commands and files. 

![image](https://user-images.githubusercontent.com/96266650/163295291-6b88f2ff-48fb-4ea8-8824-707000b8ae8b.png)
![image](https://user-images.githubusercontent.com/96266650/163295443-4bf9eec8-fbae-49c1-9c9a-f8535eede8c3.png)



