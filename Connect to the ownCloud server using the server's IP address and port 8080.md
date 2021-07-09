---


---

<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
<h1 id="connecting-to-the-owncloud-server-using-the-servers-ip-address-and-port-8080">Connecting to the ownCloud Server Using the Server’s IP address and port 8080</h1>
<p>ownCloud server can fail in detecting hostnames automatically due to bad certificates or reverse proxy like situations. Thus, you can use the following option to override the automatic detection of hostnames, for example “<a href="http://www.example.com">www.example.com</a>”, or specify the port<br>
<a href="http://www.example.com:8080">www.example.com:8080</a>.</p>
</blockquote>
<pre><code>’overwritehost’ =&gt; ’’,
</code></pre>

