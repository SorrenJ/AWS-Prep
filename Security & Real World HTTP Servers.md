

### To Do

- [x] Storing passwords
    
- [x] Encrypted cookies
    
- [x] HTTP Secure (HTTPS)
    

[HTTP to HTTPS Infographic](https://mandrillapp.com/track/click/30244704/www.brafton.com?p=eyJzIjoiUWhJUWppWVh6a0ZBLU1lZzN1OWo1ZXRsTHlFIiwidiI6MSwicCI6IntcInVcIjozMDI0NDcwNCxcInZcIjoxLFwidXJsXCI6XCJodHRwczpcXFwvXFxcL3d3dy5icmFmdG9uLmNvbVxcXC93cC1jb250ZW50XFxcL3VwbG9hZHNcXFwvMjAyNFxcXC8wNFxcXC9JbmZvZ3JhcGhpYy1Ib3ctdG8tY29udmVydC1IVFRQLXRvLUhUVFBTLXNjYWxlZC0xLnBuZ1wiLFwiaWRcIjpcImJmMmY3NjYxNTBkNTQzNzA5ZDhiYWJjZTc1ZDFiNzgxXCIsXCJ1cmxfaWRzXCI6W1wiYjBhN2QzMjdiZTYzMTMxY2VmMTMwZDk2YzBlYzY5ZWM4N2FlZDFkMlwiXX0ifQ)

### 3 Major Security Issues

- plaintext passwords
    
- plaintext cookies
    
- http is a plaintext protocol
    

// set the cookie

res.cookie('cookieName', cookieValue);

req.session.cookieName = cookieValue;

  

// reading the cookie

req.cookies.cookieName;

req.session.cookieName;

  

// clearing the cookie

res.clearCookie('cookieName');

req.session.cookieName = null; // clears one cookie

req.sesson = null; // clears all cookies

  

### Storing Passwords

- We never want to store passwords as plain text
    
- Passwords should always be hashed
    
- Hashing:
    

- The original string is passed into a function that performs some kind of transformation on it and returns a different string (the hash)
    
- This is a one way process: a hashed value cannot be retrieved
    

- We make hashing more secure by adding a salt to the original string prior to hashing
    
- This [helps to protect against Rainbow Table attacks](https://mandrillapp.com/track/click/30244704/stackoverflow.com?p=eyJzIjoic1o5T0d1dkplV3pZeE5fMDMwXy1rbDVhZURzIiwidiI6MSwicCI6IntcInVcIjozMDI0NDcwNCxcInZcIjoxLFwidXJsXCI6XCJodHRwczpcXFwvXFxcL3N0YWNrb3ZlcmZsb3cuY29tXFxcL3F1ZXN0aW9uc1xcXC80MjA4NDNcXFwvaG93LWRvZXMtcGFzc3dvcmQtc2FsdC1oZWxwLWFnYWluc3QtYS1yYWluYm93LXRhYmxlLWF0dGFja1wiLFwiaWRcIjpcImJmMmY3NjYxNTBkNTQzNzA5ZDhiYWJjZTc1ZDFiNzgxXCIsXCJ1cmxfaWRzXCI6W1wiZjVlOWRlNWE0NzUxYjU1YmI4ZjUzZmQzZDU0YTMyOWQ0YjYwYzE4Y1wiXX0ifQ)
    

### Encrypted Cookies

- Plain text cookies can be manipulated by users
    
- It's better practice to use encrypted cookies
    
- Encryption:
    

- Similar to hashing, the string is scrambled/transformed by a function
    
- This is a two-way process: encrypted strings can be decrypted by the intended recipient
    

### HTTP Secure (HTTPS)

- HTTPS uses Transport Layer Security (TLS) to encrypt communication between client and server
    
- Encrypted using asymmetric cryptography which uses a public key and private key system
    
- The public key is available to anyone who wants it and is used to encrypt the communication
    
- The private key is known only to the receiver and is used to decrypt the communication
    

### When to use...

- Plain Text Cookies:
    

- Almost never use plain cookies
    
- Maybe for:
    
- Language selection
    
- Shopping cart for non-logged in users
    
- Analytics
    

- Encrypted Cookies:
    

- Do this by default
    
- Only store a way to uniquely identify the user (eg. user_id or username can be used to look up values in a database or object)
    

### Useful Links

- [Plain Text Offenders](https://mandrillapp.com/track/click/30244704/github.com?p=eyJzIjoiTHBLLWdIUXZ3THpxbFZJeGc3UzlySzNpX3M0IiwidiI6MSwicCI6IntcInVcIjozMDI0NDcwNCxcInZcIjoxLFwidXJsXCI6XCJodHRwczpcXFwvXFxcL2dpdGh1Yi5jb21cXFwvcGxhaW50ZXh0b2ZmZW5kZXJzXFxcL3BsYWludGV4dG9mZmVuZGVyc1xcXC9ibG9iXFxcL21hc3RlclxcXC9vZmZlbmRlcnMuY3N2XCIsXCJpZFwiOlwiYmYyZjc2NjE1MGQ1NDM3MDlkOGJhYmNlNzVkMWI3ODFcIixcInVybF9pZHNcIjpbXCI2NDE2ZGJmZTQ0Mzg0ZDIyOGEwM2YwNGMyMTc0ZTk3MGEwYjM0NzRiXCJdfSJ9)
    
- [How Does Encryption Work?](https://mandrillapp.com/track/click/30244704/medium.com?p=eyJzIjoibjhuZXEycUt6anB3OXpmQ2ItNE5mdVFVbk5vIiwidiI6MSwicCI6IntcInVcIjozMDI0NDcwNCxcInZcIjoxLFwidXJsXCI6XCJodHRwczpcXFwvXFxcL21lZGl1bS5jb21cXFwvc2VhcmNoZW5jcnlwdFxcXC93aGF0LWlzLWVuY3J5cHRpb24taG93LWRvZXMtaXQtd29yay1lOGYyMGUzNDA1MzdcIixcImlkXCI6XCJiZjJmNzY2MTUwZDU0MzcwOWQ4YmFiY2U3NWQxYjc4MVwiLFwidXJsX2lkc1wiOltcImNlOTRhMDJmYWEwMDEyNTViNGU2NGUwZTliZDNlOTc2NmE4OTI4MmJcIl19In0)
    
- [What is HTTPS?](https://mandrillapp.com/track/click/30244704/www.cloudflare.com?p=eyJzIjoiSGd3TWprSGU5VUt3ZXhvSkoxUUl0eHhtT21FIiwidiI6MSwicCI6IntcInVcIjozMDI0NDcwNCxcInZcIjoxLFwidXJsXCI6XCJodHRwczpcXFwvXFxcL3d3dy5jbG91ZGZsYXJlLmNvbVxcXC9sZWFybmluZ1xcXC9zc2xcXFwvd2hhdC1pcy1odHRwc1xcXC9cIixcImlkXCI6XCJiZjJmNzY2MTUwZDU0MzcwOWQ4YmFiY2U3NWQxYjc4MVwiLFwidXJsX2lkc1wiOltcImZjNjQwZTY3N2E2NDEzMjYzMGZjOWE1OTVlMGRhMjMyOGQyMzM4MWVcIl19In0)
    
- [Asymmetric Cryptography](https://mandrillapp.com/track/click/30244704/searchsecurity.techtarget.com?p=eyJzIjoiQ0pVWGk3VUxtaE5ZU09OMDhtU2dZbGU1dmo4IiwidiI6MSwicCI6IntcInVcIjozMDI0NDcwNCxcInZcIjoxLFwidXJsXCI6XCJodHRwczpcXFwvXFxcL3NlYXJjaHNlY3VyaXR5LnRlY2h0YXJnZXQuY29tXFxcL2RlZmluaXRpb25cXFwvYXN5bW1ldHJpYy1jcnlwdG9ncmFwaHlcIixcImlkXCI6XCJiZjJmNzY2MTUwZDU0MzcwOWQ4YmFiY2U3NWQxYjc4MVwiLFwidXJsX2lkc1wiOltcImY4ZDAwNWI1NjUzYmY1MDY4OWViZTMwMzViZDdmN2M4ODAwYjU0MThcIl19In0)
    
- [Client Session vs Server Session](https://mandrillapp.com/track/click/30244704/www.rodsonluo.com?p=eyJzIjoiWm9VVU00R0M2UGlBR3dSMXVoUExLcm1DbUJzIiwidiI6MSwicCI6IntcInVcIjozMDI0NDcwNCxcInZcIjoxLFwidXJsXCI6XCJodHRwOlxcXC9cXFwvd3d3LnJvZHNvbmx1by5jb21cXFwvY2xpZW50LXNlc3Npb24tdnMtc2VydmVyLXNlc3Npb25cIixcImlkXCI6XCJiZjJmNzY2MTUwZDU0MzcwOWQ4YmFiY2U3NWQxYjc4MVwiLFwidXJsX2lkc1wiOltcIjAxNjA1Mzk1MmZjZDFhMzViNDAwNTA2YjMyMzlmMzhmYzU5MTc1N2ZcIl19In0)
    

---

[View on Compass](https://mandrillapp.com/track/click/30244704/web.compass.lighthouselabs.ca?p=eyJzIjoiT1hGY0Rzd0dreEdwSE1iT1hMSGVxUDFYVFZnIiwidiI6MSwicCI6IntcInVcIjozMDI0NDcwNCxcInZcIjoxLFwidXJsXCI6XCJodHRwczpcXFwvXFxcL3dlYi5jb21wYXNzLmxpZ2h0aG91c2VsYWJzLmNhXFxcL2FjdGl2aXRpZXNcXFwvOTE2XFxcL2xlY3R1cmVzXFxcLzgwMTlcIixcImlkXCI6XCJiZjJmNzY2MTUwZDU0MzcwOWQ4YmFiY2U3NWQxYjc4MVwiLFwidXJsX2lkc1wiOltcImZiYWM3MTQ2MWU0ZDE3NDcyNjAwYWE3NWUxNmYwM2Y0NThjN2JkZmZcIl19In0) | [Leave Feedback](https://mandrillapp.com/track/click/30244704/web.compass.lighthouselabs.ca?p=eyJzIjoiWm05dFFwLUpWaEZnSTg1Q2pKOWpPMWNWQlpFIiwidiI6MSwicCI6IntcInVcIjozMDI0NDcwNCxcInZcIjoxLFwidXJsXCI6XCJodHRwczpcXFwvXFxcL3dlYi5jb21wYXNzLmxpZ2h0aG91c2VsYWJzLmNhXFxcL2ZlZWRiYWNrc1wiLFwiaWRcIjpcImJmMmY3NjYxNTBkNTQzNzA5ZDhiYWJjZTc1ZDFiNzgxXCIsXCJ1cmxfaWRzXCI6W1wiMjgyNjc0MmMwM2MwYzM0YmM3NjJhN2UzOWE1YzAzYzk2NjMwMmE5NFwiXX0ifQ)

**