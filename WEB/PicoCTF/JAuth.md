![image](https://github.com/nhattanhh/CTF/assets/130430279/a8e7fcc2-4cff-42c6-ae64-8c0f92fde8eb)


![image](https://github.com/nhattanhh/CTF/assets/130430279/a38e7f5d-b8f5-4317-8e9f-2bfcc28a65da)


Okay! Login with test-Test123 and we get the token.


![image](https://github.com/nhattanhh/CTF/assets/130430279/53c66c5a-6533-45fe-928b-9bed0ee118be)


Try decode with jwt.io, let see that...


![image](https://github.com/nhattanhh/CTF/assets/130430279/d026a95a-561d-45b5-8ad7-e7a9409a268c)


Hm! Just change the value of "alg" to "none" and "role" to "user" like this:
I can't change the value of "alg" to "none" with jwt.io page, change to https://token.dev/ to change it.


![image](https://github.com/nhattanhh/CTF/assets/130430279/41103eac-5409-4a5f-b119-90809577957e)


Add to cookie again and don't forget to add '.' dot after all jwt code heheeh~.~


![image](https://github.com/nhattanhh/CTF/assets/130430279/8f98d49d-7843-41b2-beac-9c36b287508b)

Done!
