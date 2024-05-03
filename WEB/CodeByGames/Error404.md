![image](https://github.com/nhattanhh/CTF/assets/130430279/1add84b0-1365-41e1-9db1-02bce8f0aeeb)

- Look at the title, we will immediately think of problems when the website has a 404 error.

- So let make it.

![image](https://github.com/nhattanhh/CTF/assets/130430279/193664da-3686-4976-b994-ca5c1b3dff57)

![image](https://github.com/nhattanhh/CTF/assets/130430279/5e660d3f-1f56-4968-91eb-69caab92469a)

- I will change to another url and see what we got here.

![image](https://github.com/nhattanhh/CTF/assets/130430279/94cbcee7-138f-456e-9f2f-729edfcac77f)

- Ok! This line has changed, i try to XSS but it has filter.

![image](https://github.com/nhattanhh/CTF/assets/130430279/94e5a4b9-7199-419a-8eef-a79e9af6da00)

- Try another and i see that i can use SSTI.

![image](https://github.com/nhattanhh/CTF/assets/130430279/51420a89-50c3-43e4-83b8-366c31ab4ee6)

- So use this payload to get the flag, flag will be hidden in ~/root/flag.txt~

- #%7B%7B%20config.__class__.from_envvar.__globals__.__builtins__.__import__("os").popen("cd%20..;cd%20root;cat%20flag.txt").read()%20%7D%7D#

![image](https://github.com/nhattanhh/CTF/assets/130430279/0bec9bd2-1c5b-437c-8ebc-2ea1cdf3c4d5)
