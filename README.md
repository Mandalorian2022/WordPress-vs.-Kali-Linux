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
  This vulnerability was exploited by msfconsole by searching for specific exploit in the databse. 
![Exploit2](https://user-images.githubusercontent.com/96266650/163274154-47a1fa3b-e536-442f-ba85-a64ab71421a7.png)

3- Reflex Gallery - jQuery prettyPhoto DOM Cross-Site Scripting (XSS)
