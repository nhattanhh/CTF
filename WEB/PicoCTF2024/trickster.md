![image](https://github.com/nhattanhh/CTF/assets/130430279/ac1bd467-9ce0-4855-b7c6-c887d04370b7)

Try to post png file and contain php, like .png.php ut it not work. I have investigated that:

![image](https://github.com/nhattanhh/CTF/assets/130430279/07f417b7-9d44-4d5c-9e6e-770e2ae72b31)

Okay, those bytes it is spitting back at us are the first bytes of our file, these do not match the first bytes of a png file. Since it's complaining about the file header not matching the file header of a png file, what if we force some png bytes into the beginning of our file. According to Wikipedia every png starts with the hex bytes: 89 50 4e 47 0d 0a 1a 0a. We create a file with these bytes

