# Extra: Web Security

The Internet sees most communications that happen daily,
and the amount of information passed is enormous.
Any security breach can result in economic consequences.
Thus it is important to take measures to protect both end users and servers.

## Browser Policies

Most browsers implement standard security policies
to protect end users from malicious attacks from sites
other than the one that is being displayed.

### Same-Origin Policy

[Wikipedia link](https://en.wikipedia.org/wiki/Same-origin_policy)

[MDN doc](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)

When a webpage contains multiple documents (iframes),
scripts on one page can only access the other page if they are from the same origin.
This allows a page to safely embed documents from other sites
without the need to worry that malicious scripts might alter the page itself.

### Cross-Origin Resource Sharing (CORS)

[MDN doc](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

## Common Vulnerabilities

There are some common vulnerabilities that every web developer should be aware of,
and protect against when developing web servers.

### SQL Injection

SQL injection can happen when raw user input is used in SQL statements.
Certain crafted user input can change the nature of the SQL statement and result in data breaches or losses.

For example,

```python
sql = "SELECT * FROM users WHERE username = '" + username + "' AND password = '" + password + "';"
```

This is a common SQL statement for user logins.
However, if we have username input as `admin'; --`,
the result becomes

```sql
SELECT * FROM users WHERE username = 'admin'; --' AND PASSWORD = '';
```

Note that `--` is comment in SQL,
so this new sql will select the user "admin" if there is one (and there usually is).

[Related](https://beta.companieshouse.gov.uk/company/10542519)

To protect against SQL injection,
the most common practice is to clean user inputs before using them in the SQL statement.
Some libraries, like SqlAlchemy or Django, has built-in input cleaning,
so it's always preferable to use the ORM over raw SQL.

### Cross-Site Request Forgery (CSRF)

When a browser sends a request,
it will look the same whether the request is sent by the end user or by a malicious script.
Since cookies work on a per-domain basis and will always be included,
a malicious site can send a request from the end user's browser without user action,
and result in transactions that are not intended by the user.

For example, a bank site looks for this request:

```
POST /transfer?recipient_id={}&amount={}
```

where the user making the transfer will be indicated by cookies.

This works just fine when the user visits the bank website and fill out a form.
However, another site can also send the exact same request,
with `recipient_id` pointing to a certain account, and an arbitrary amount,
from the user's browser,
either by tricking the user to click on a button or just using some scripts.
This will result in users that have logged into the bank website
and visit the malicious site at the same time to lose money.

To protect against CSRF,
the most common practice is to include a random token on the page
where the user fills the form (`GET /transfer`),
so that legitimate requests by the user will include that token,
which can be checked by the server.
Since the token is only included in the GET request and same-origin policy is in play,
malicious sites do not have any way to access that token.

### Cross-Site Scripting (XSS)

When a site displays user input on the website,
it is possible that the user input contains malicious input,
and will result in unwanted results when others visit the site.

It's especially important when the user input contains formatting,
and comes in as raw HTML.
If there is a `<script>` tag and it is included as-is in on the page,
the browser will treat it just as any script on the page and execute it.

It is also possible for the input to include an end tag and mess up the HTML structure.

To protect against XSS,
the most common practice is to sanitize the user input and disable certain tags,
as well as to check the HTML structure.
