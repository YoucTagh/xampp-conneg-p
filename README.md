# Content Negotiation by Profile for XAMPP Server

For each example e.g. [example1](/cnp/examples/example1). we have three main components. 
* a configuration file e.g. [.htaccess](/cnp/examples/example1/.htaccess)
* a default representation e.g. [available-profiles.html](/cnp/examples/example1/available-profiles.html)
* the different representations e.g. [onto.profile1.ttl](/cnp/examples/example1/onto.profile1.ttl)

### The Configuration File

It follows this template:

```cgi
FallbackResource /cnp/examples/example1/available-profiles.html


RewriteEngine On 
RewriteCond %{REQUEST_URI}  ^\/cnp\/examples\/example1\/$ 
RewriteCond %{QUERY_STRING} ^_profile=profile1$ 
RewriteRule ^(.*)$ http://localhost:80/cnp/examples/example1/onto.profile1.ttl [R=303]

RewriteCond %{REQUEST_URI}  ^\/cnp\/examples\/example1\/onto.profile1.ttl$ 
RewriteCond %{QUERY_STRING} ^_profile=profile1$    
RewriteRule ^ %{REQUEST_URI}? [R,L]
```

First we define the default representation. Then we redirect to the right representation according to the provided *Query String Argument*. Here we use the `_profile` key/value pair to convey the needed profile.
