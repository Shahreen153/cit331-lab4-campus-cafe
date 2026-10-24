# HTTP observations (Lab 4, Task 1)

| Question | My answer |
|----------|-----------|
| Request method for index.html | GET |
| Status code with Disable cache ticked | 200 OK |
| Status code on a normal reload | 304 |
| Status code for /nothing-here.html | 404 |
| Value of the Content-Type response header | text/html; charset=UTF-8 |
| Remote Address (IP and port) | 127.0.0.1:5500 |
| Protocol in the address bar (http or https) | http |

## Why is this address http and not https?

HTTPS encrypts data that travels across a network, but traffic to 127.0.0.1 never leaves my own computer, so nobody can intercept it. Live Server is only a local development server, so it does not need a certificate or encryption.



## Form validation test (Lab 4, Task 3)

| Input | What the browser did |
|-------|----------------------|
| Name left empty | A bubble said "Please fill out this field" and the form was not sent. |
| Name: Al | The browser asked for at least 3 characters and blocked the form. |
| Phone: 12345 | The browser showed my title hint (11 digits starting with 03, for example 03001234567) and blocked the form. |
| Phone: 03001234567 | The phone number was accepted with no error. |
| Quantity: 0 or 11 | The browser said the value must be at least 1 (for 0) or at most 10 (for 11). |
| Pickup time: 07:30 or 19:00 | The browser said the time must be between 08:00 and 18:00. |
| Item left on "Choose an item..." | The browser said "Please select an item in the list". |

With all fields valid, the page reloaded and `#` was added to the address because of action="#". JavaScript will stop this in the next step.



## Order feature test (Lab 4, Task 3)

I placed an order for Shahreen Qasim (Cafe Latte, Medium, quantity 1, pickup 14:59, extra: Whipped cream). The page did not reload, a thank-you message appeared, and the order was shown in the Saved orders table. The order was still there after refreshing the page, which shows it is stored in localStorage and not in a variable.

## XSS challenge (Lab 4, Task 3)

When I entered the name `<b>Test</b>`, the table showed the characters exactly as typed, with the angle brackets visible and no bold text. This happens because the code uses textContent, which treats the text as plain text and never as HTML.

If the code had used row.innerHTML = "<td>" + order.name + "</td>" instead, an attacker could type a name such as `<img src=x onerror="alert('hacked')">`. The browser would treat it as real HTML and run the script. This attack is called XSS (cross-site scripting).


## Specificity experiment

When I added `#main p { color: red; }`, the hero paragraph turned red even though `.hero p` comes earlier in the file, because an id selector (1,0,1) has higher specificity than a class plus an element (0,1,1). When I changed it to `main p` (0,0,2), the hero paragraph went back to white because `.hero p` (0,1,1) beats it.

## Selectors I used

| Selector kind | Example from my CSS |
|---------------|---------------------|
| Element | `body` |
| Class | `.hero` |
| ID | `#main` |
| Grouping (comma) | `h1, h2, h3` |
| Descendant (space) | `.nav-list a` |
| Child (>) | `main > section` |
| Adjacent sibling (+) | `h1 + p` |
| Compound (no space, such as a.active) | `.nav-list a.active` |
| Attribute | `a[href^="http"]` |
| Pseudo-class | `a:hover` |
| Pseudo-element | `.menu-group h2::before` |

## Bug log (Lab 4, Task 6)

| # | What was wrong (file and line) | Which tool showed it | My fix |
|---|--------------------------------|----------------------|--------|
| 1 | bugs.html head: link pointed to style.css but the file is bugs.css | Network tab (404) | Changed href to bugs.css |
| 2 | bugs.html: <html> had no lang attribute | Lighthouse, W3C validator | Added lang="en" |
| 3 | bugs.html: <img> had no alt text | Lighthouse | Added alt="Campus Café logo" |
| 4 | bugs.html: label for="mail" did not match input id="email" | Lighthouse | Changed for to "email" |
| 5 | bugs.html: navigation was a <div class="menu"> not a <nav> | Accessibility tree | Replaced div with nav |
| 6 | bugs.html: h1 followed directly by h4 (skipped levels) | Accessibility tree, validator | Changed h4 to h2 |
| 7 | bugs.css .btn: property "colour" is misspelled | Styles pane | Changed to color |
| 8 | bugs.css .btn:hover: missing semicolon after background, so cursor was ignored | Styles pane | Added ; |
| 9 | bugs.css: selector .notes, but the HTML class is note | Styles pane | Renamed selector to .note |
| 10 | bugs.css .note: #999999 on white has too little contrast | Lighthouse (second run) | Changed to #595959 |

## Live site observations (Lab 4, Task 7)

1. On localhost the protocol was http, the server was Live Server and the Remote Address was 127.0.0.1:5500. On the live site the protocol is https (h2), the server header is GitHub.com and the Remote Address is 185.199.111.153:443. It changed because the live site runs on GitHub's servers across the internet, and the traffic is encrypted with HTTPS.
2. The padlock shows the connection is encrypted and the certificate (issued by Let's Encrypt, valid from 30 September 2026 to 29 December 2026) proves the site really is github.io. On plain http, an attacker on the same Wi-Fi could read or change the data, such as orders typed in the form.
3. localStorage belongs to an origin (protocol + host + port). localhost:5500 and shahreen153.github.io are different origins, so the live site could not see the orders saved on localhost.
4. The missing page returned status 404, and it was sent by GitHub's server (GitHub Pages), not by my own code.