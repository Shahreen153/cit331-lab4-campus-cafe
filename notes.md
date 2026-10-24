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