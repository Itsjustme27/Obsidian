


![](https://miro.medium.com/v2/resize:fit:700/1*q0kfmq28YTLivE1fPZ_qAA.jpeg)

> An accounting team receives an urgent payment request from a known vendor. The email appears legitimate but contains a suspicious link and a .zip attachment hiding malware. Your task is to analyze the email headers, and uncover the attacker’s scheme.

**Task 1: What is the originating IP address of the sender?**

In my opinion, one of the best websites for analyzing emails is  
[https://eml-analyzer.herokuapp.com](https://eml-analyzer.herokuapp.com)

I uploaded the file to the site and initiated the analysis.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*2K1BdT91QfrIJKWKTGR3yg.png)

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*A2Dp-Xt-KlqrHS7Yr9l5sw.png)

> **Answer Task 1_:_** 45.67.89.10

**Task 2: Which mail server relayed this email before reaching the victim?**

The headers show the final hop before the victim’s server (`mail.target.com`) came from **mail{.}business-finance{.}com (20.3.113.25)**, making it the last relay.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*NbyLxH8KRQieI5AFhUI79g.png)

> **Answer Task 2:** 203.0.113.25

**Task 3: What is the sender’s email address?**

Every email header has a “**From”** field, which specifies the sender’s claimed email address.

The sender’s email address is “**finance@business-finance{.}com”**

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*RM3OT6iVSBhX7gvwURq4mg.png)

> **Answer Task 3:** finance@business-finance{.}com

**Task 4: What is the ‘Reply-To’ email address specified in the email?**

The **“Reply-To”** field overrides that when you hit “Reply” in the mail client, meaning replies won’t go back to the visible sender but instead to `support{@}business-finance{.}com`.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*-ueUXv1SPCjOyBhgZZgnsQ.png)

> **Answer Task 4:** support@business-finance{.}com

**Task 5: What is the SPF (Sender Policy Framework) result for this email?**

**SPF (Sender Policy Framework)** verifies if the sending server’s IP is authorized by the domain, and in this case the result is **Pass** because `45.67.89.10` is listed in the SPF record for `business-finance{.}com`, meaning the email came from an approved server.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*hoORay8FnIuIYJ2QXzdilA.png)

> **Answer Task 5:** Pass

**Task 6: What is the domain used in the phishing URL inside the email?**

The phishing URL **“hXXps{:}//secure{.}business-finance{.}com/invoice/details/view/INV2025–0987/payment”** uses the domain “**secure{.}business-finance{.}com”.**

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*g2_QxmIk9XlhmbPQ6UiP1Q.png)

> **Answer Task 6:** secure.business-finance.com

**Task 7: What is the fake company name used in the email?**

The fake company name used in the email is “**Business Finance Ltd.”**

Attackers often use **generic but professional-sounding company names** to appear legitimate and pressure victims into paying fake invoices or clicking malicious links.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*pvz1fzlgTSiSkouCNufc8A.png)

> **Answer Task 7:** Business Finance Ltd.

**Task 8: What is the name of the attachment included in the email?**

The attachment is named “**Invoice_2025_Payment.zip”**, a suspicious invoice-themed ZIP file often used in phishing to hide malicious payloads and trick victims into opening it.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*7WX5Ya0ikUEZbGfjAmkx1A.png)

> **Answer Task 8:** Invoice_2025_Payment.zip

**Task 9: What is the SHA-256 hash of the attachment?**

The SHA-256 hash of the attachment “**Invoice_2025_Payment.zip”** is **8379C41239E9AF845B2AB6C27A7509AE8804D7D73E455C800A551B22BA25BB4A**, which uniquely identifies this file and can be used to check threat intelligence databases or sandboxes for known malware.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*OaBUw210qWWXCCa1cvMqyA.png)

**Answer Task 9:** 8379C41239E9AF845B2AB6C27A7509AE8804D7D73E455C800A551B22BA25BB4A

> **Task 10: What is the filename of the malicious file contained within the ZIP attachment?**

Let’s download the ZIP attachment and transfer it to a Linux machine to unzip and examine its contents.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:1000/1*8mfDOZ8vzbEQ4QBq21ArTw.png)

The malicious file inside the ZIP attachment is named “**invoice_document.pdf.bat”**, a deceptive filename designed to appear like a harmless PDF but actually executes as a Windows batch file, a common phishing technique to trick victims into running malware.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*ZtDfqk-_2niMzgYKNfsBxA.png)

> **Answer Task 10:** invoice_document.pdf.bat

**Task 11: Which MITRE ATT&CK techniques are associated with this attack?**

The MITRE ATT&CK technique associated with this attack is **T1566.001 -Phishing: Spearphishing Attachment**, because the malicious email delivered a ZIP file (`Invoice_2025_Payment.zip`) containing a disguised executable, which is a classic example of using an attachment in phishing to gain initial access.

> **Answer Task 11:** T1566.001

**DONE!**

Key Phishing Awareness Takeaways:

1. **Verify the sender** — Ensure the domain and display name are legitimate.
2. **Inspect URLs** — Hover over links to confirm the true destination before clicking.
3. **Examine attachments carefully** — Treat unexpected ZIP, EXE, BAT, or macro-enabled Office files as high risk.
4. **Recognize social engineering** — Watch for emails that create urgency, fear, or pressure to act quickly.