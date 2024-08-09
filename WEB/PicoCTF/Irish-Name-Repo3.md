- OK! now in admin login page, we only have to bypass by password.

![image](https://github.com/user-attachments/assets/46b06f6e-52d6-42a2-85b1-f0afd8ab672c)

- Try to think for a moment, the solution of 2 challs before doesn't work anymore...

![image](https://github.com/user-attachments/assets/6f8b706b-5aa0-41c0-ae66-7c1cd94ab2de)

- The hints say the password is encrypted.

- Change the debug from 0 to 1, you will see the query.

![image](https://github.com/user-attachments/assets/c9708e86-89d4-42e9-9929-ac86935e3a00)

- 'or' will be encrypted to 'be', there will be alphabet will be encrypted, try with ' be 1=1 --  , i wonder how it will be encrypted...

- Oh! 'be' will be encrypted to 'or' and this is the flag...

![image](https://github.com/user-attachments/assets/757fe9f2-6c82-46db-ba86-3cddb6dd8d04)
