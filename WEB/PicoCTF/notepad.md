  NOTEPAD

- Download notepad.tar and unzip it, we see that:
    + In long_content.html, it will print error notice when our length over 512 characters.
      
    + In app.py:
      
  ![image](https://github.com/nhattanhh/CTF/assets/130430279/07328aeb-1af0-4829-81c7-b6040e51b38f)

    -> we can't use "_" and "/" to type in 'content' parameters.

-> So let test this, when i type aaaa:   -> https://notepad.mars.picoctf.net/static/aaaa-wnvKxaKpfXU.html

  ![image](https://github.com/nhattanhh/CTF/assets/130430279/36d6c4ec-8720-4f09-9563-38676e7bc8b5)

- The filename is the first 128 characters of the content and a random token
  
- Hmm, let see if we use "_" of "/", what it will print out.
  
  ![image](https://github.com/nhattanhh/CTF/assets/130430279/e090de88-20f6-4e72-abf2-b313a1aa1032)

-> https://notepad.mars.picoctf.net/?error=bad_content -> Oh! parameter 'error', return to source code and see it:

  ![image](https://github.com/nhattanhh/CTF/assets/130430279/97c5dec8-6cee-4b01-94d0-2690b649aa8f)

  -> Now we can use Server-Side Template Injection(SSTI):

  - First, write ..\template\errors\test:

    ![image](https://github.com/nhattanhh/CTF/assets/130430279/9ec2c956-3149-4ebd-af06-bc50ef5f8b9b)

    And we got:

    ![image](https://github.com/nhattanhh/CTF/assets/130430279/fa854894-b84f-471c-ace5-8d9482d8bc20)

    -> Successful inject, now paste filename to error parameter :

    ![image](https://github.com/nhattanhh/CTF/assets/130430279/486d8d79-fa4b-43f0-944a-a87967ff6049)

    BOOM:

    ![image](https://github.com/nhattanhh/CTF/assets/130430279/f5ae1060-38ca-47c5-9f5f-b87ca87ed009)

    - Face to jinja, find payload RCE on hacktricks:  ..\..\..\..\..\..\..\..\..\..\..\..\app\templates\errors\aa{% with a = request["application"]["\x5f\x5fglobals\x5f\x5f"]["\x5f\x5fbuiltins\x5f\x5f"]["\x5f\x5fimport\x5f\x5f"]("os")["popen"]("echo -n bHM | base64 -d | bash")["read"]() %}{{a}}{% endwith %}

      -> Try this for RCE, open file from errors parameter and keep going... for this: picoCTF{styl1ng_susp1c10usly_s1m1l4r_t0_p4steb1n}

