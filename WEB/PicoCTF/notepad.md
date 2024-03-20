  NOTEPAD

- Download notepad.tar and unzip it, we see that:
    + In long_content.html, it will print error notice when our length over 512 characters.
    + In app.py:
    + 
  ![image](https://github.com/nhattanhh/CTF/assets/130430279/07328aeb-1af0-4829-81c7-b6040e51b38f)

    -> we can't use "_" and "/" to type in 'content' parameters.

-> So let test this, when i type aaaa:   -> https://notepad.mars.picoctf.net/static/aaaa-wnvKxaKpfXU.html

  ![image](https://github.com/nhattanhh/CTF/assets/130430279/36d6c4ec-8720-4f09-9563-38676e7bc8b5)

- The filename is the first 128 characters of the content and a random token
- Hmm, let see if we use "_" of "/", what it will print out.
- 
  ![image](https://github.com/nhattanhh/CTF/assets/130430279/e090de88-20f6-4e72-abf2-b313a1aa1032)

-> https://notepad.mars.picoctf.net/?error=bad_content -> Oh! parameter 'error', return to source code and see it:

  ![image](https://github.com/nhattanhh/CTF/assets/130430279/97c5dec8-6cee-4b01-94d0-2690b649aa8f)

  -> Try to exploit from this with Server-Side Template Injection(SSTI):

  


