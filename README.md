# Some Simple Security Tips

## Click jacking

Protect yourself with frame killing javascript snippets that says they do not wanted to be included in foreign frames. 

```javascript
<script>
if (self == top) {
  // Everything checks out, show the page.
   document.documentElement.style.display = 'block';
 } else {
   // Break out of the frame.
   top.location = self.location;
 }
</script>
```

You can use the X-Frame-Options HTTP header to indicate whether a browser should be allowed to render a page in a `<frame>`, `<iframe>`, or `<object>` tag. There are three values: DENY, SAMEORIGIN, ALLOW-FROM url.

Content Security Property HTTP header gives web developers a way to whitelist individual domains from which resources can be loaded and also domains that are permitted to embed a page.

```
Content-Security-Policy: frame-ancestors ‘none’ ‘self’ or uri
```

Use setHeader in Node, headers for Ruby and pass in the values.

## Cross Site Scripting

1. Escape Dynamic Content. Make it so that raw javascript cannot be injected into input areas. Escaping editable content is this way means that it will never be treated as executable code. 
2. You can whitelist only particular values in the input, for instance, letting people choose from a dropdown or using regular expressions to validate input.
3. Sanitize HTML inputs.

## SQL Injection

1. Parameterized statements make sure that the parameters passed into SQL queries are treated in a safe manner. 
2. Not concatenating input strings to SQL statements.
3. Escaping symbol characters in the inputs. 
4. Sanitize inputs by matching it with regular expressions. Ensure numeric or alphabetical fields do not contain special characters. Reject out whitespace and new line characters.

## Session Fixation

1. Don’t pass session IDs in GET/POST variables. Session ids are better passed through HTTP cookies.
2. Regenerate Session IDs at authentication. 
3. Accept only server generated session ids. Timeout and replace old session ids. 
4. Implement a strong logout function. Require a new session when visiting from suspicious referrers.
