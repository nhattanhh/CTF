* This is basic chall of cmd injection:

![image](https://github.com/nhattanhh/CTF/assets/130430279/2bc61b15-9896-42d8-9537-f4e2cdabb6c3)

* Check source code, we see:

![image](https://github.com/nhattanhh/CTF/assets/130430279/b321dc7c-af5a-484f-9703-1a2f2ecf8de2)

- /assets/image?name=spongebob&size=999x200
- /assets/image?name=house&size=300x494

* That's same, pick 1 and access that:

![image](https://github.com/nhattanhh/CTF/assets/130430279/73d9fc3e-04e9-4c90-993f-ebef361750cd)

If i change the name to other that invalid name, i will be responded by an error, but when i change back again the name and try cmd injection with size, i got this:

![image](https://github.com/nhattanhh/CTF/assets/130430279/746c11db-796e-4761-899e-f1f963df8868)

It mean that after our command, we have '!' behind, by pass like this and get the flag...

![image](https://github.com/nhattanhh/CTF/assets/130430279/93ba0c03-3d7e-4856-b21f-72710b15b678)
