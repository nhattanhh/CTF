![image](https://github.com/nhattanhh/CTF/assets/130430279/ac1bd467-9ce0-4855-b7c6-c887d04370b7)

Try to post png file and contain php, like .png.php ut it not work. I have investigated that:

![image](https://github.com/nhattanhh/CTF/assets/130430279/54ccf126-61ff-4cf3-8f64-97acce74a4ff)


![image](https://github.com/nhattanhh/CTF/assets/130430279/7d14a4ee-de34-4622-919b-c150fd708e3b)


Okay, those bytes it is spitting back at us are the first bytes of our file, these do not match the first bytes of a png file. Since it's complaining about the file header not matching the file header of a png file, what if we force some png bytes into the beginning of our file. According to Wikipedia: https://en.wikipedia.org/wiki/List_of_file_signatures . Every png starts with the hex bytes: 89 50 4e 47 0d 0a 1a 0a. We create and download it, i called: hacklord.png

![image](https://github.com/nhattanhh/CTF/assets/130430279/a7674c95-769d-4fb6-8e1c-58b167a48f27)

Ok we have png signature here, now we will inject basic php code by notepad and rename to hacklord.png.php to RCE that:

![image](https://github.com/nhattanhh/CTF/assets/130430279/74cb30e8-9c1b-4283-9cca-d9195c8ad373)

![Ảnh chụp màn hình 2024-04-08 231136](https://github.com/nhattanhh/CTF/assets/130430279/e1727ecf-c1b4-4942-a544-9fe01e5279ad)


Got its!

![image](https://github.com/nhattanhh/CTF/assets/130430279/01066d8a-bc93-4727-bfcb-d212164ddfd9)

Access to php file with /uploads/hacklord.png.php and RCEEEEEEEEEEEEEEEEE...

![image](https://github.com/nhattanhh/CTF/assets/130430279/31a4cd63-e1ff-4540-b67d-35d677ee7f1f)

nikeee!

![image](https://github.com/nhattanhh/CTF/assets/130430279/20b09819-9cd3-41be-8f75-8ed429853847)

![image](https://github.com/nhattanhh/CTF/assets/130430279/08bf185a-cb81-42a6-9ac0-ed8ab6479848)
