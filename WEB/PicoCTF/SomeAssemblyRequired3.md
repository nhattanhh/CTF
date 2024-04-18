![image](https://github.com/nhattanhh/CTF/assets/130430279/4b0705f1-0968-4abd-95d0-f2a7425edfb1)


- Check source and we get some code here.
  
- I search for it and know that it related to XOR to decode.
  
- Write a python code to decode that:
  

  /*d_1024="\x9dn\x93\xc8\xb2\xb9A\x8b\x90\xc2\xddc\x93\x93\x92\x8fd\x92\x9f\x94\xd5b\x91\xc5\xc0\x8ef\xc4\x97\xc0\x8f1\xc1\x90\xc4\x8ba\xc2\x94\xc9\x90\x00\x00";
  d_1067="\xf1\xa7\xf0\x07\xed";
  for i in range(len(d_1024)): 
    print(chr(ord(d_1024[i])^ord(d_1067[4-(i%5)])),end="")*/


  ![image](https://github.com/nhattanhh/CTF/assets/130430279/2d9cf36a-8539-472f-af78-4196031f873d)


- Run it and get the flag.
