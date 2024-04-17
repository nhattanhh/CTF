Let see what we got here!

![image](https://github.com/nhattanhh/CTF/assets/130430279/e6a7b41a-f314-418a-9d83-8d36e86a0939)

we can't login as 'admin', try with 'John' and we will see the cookie adter that...

![image](https://github.com/nhattanhh/CTF/assets/130430279/c3b05911-b7ac-4e09-8319-5fd5b6b19ed2)

Hmm! jwt code. Now download 'John The Ripper' tool in 'John' in bottom of the page with this git link: https://github.com/openwall/john

![image](https://github.com/nhattanhh/CTF/assets/130430279/a92013ce-2d04-458a-8475-3e42e3e2755a)

- create file with jwt code in cookie, here i called jwt.

- use  "john jwt --show" command and you will got this:

![image](https://github.com/nhattanhh/CTF/assets/130430279/3ade124c-75dc-4efe-9129-de2829fe053a)

use this secret with jwt.io by this way:

![image](https://github.com/nhattanhh/CTF/assets/130430279/620b411a-351f-4011-a0be-6369470e4170)

Add again to cookie and BOOM!:

![image](https://github.com/nhattanhh/CTF/assets/130430279/3d77591a-068f-4413-b533-8ed20a81ea37)

flag for ouR...
