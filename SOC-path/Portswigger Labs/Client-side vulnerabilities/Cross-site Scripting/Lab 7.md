# Lab: Reflected XSS into attribute with angle brackets HTML-encoded

This lab contains a reflected cross-site scripting vulnerability in the search blog functionality where angle brackets are HTML-encoded. To solve this lab, perform a cross-site scripting attack that injects an attribute and calls the `alert` function.

#### Hint

Just because you're able to trigger the `alert()` yourself doesn't mean that this will work on the victim. You may need to try injecting your proof-of-concept payload with a variety of different attributes before you find one that successfully executes in the victim's browser.



## Write-up

1) So for the first time, i solved this lab by myself here is what i did.
2) 1. Submit a random alphanumeric string in the search box, then use Burp Suite to intercept the search request and send it to Burp Repeater.
3. Observe that the random string has been reflected inside a quoted attribute.
4. Replace your input with the following payload to escape the quoted attribute and inject an event handler:
    `"onmouseover="alert(1)`
4. Verify the technique worked by right-clicking, selecting "Copy URL", and pasting the URL in the browser. When you move the mouse over the injected element it should trigger an alert.