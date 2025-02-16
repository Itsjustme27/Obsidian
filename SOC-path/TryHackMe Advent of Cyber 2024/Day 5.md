Day 5 : SOC-mas XX-what-ee?

Learning Objectives

- Understand the basic concepts related to XML![XML handling data like a file drawer.](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1730189972624.png)
- Explore XML External Entity (XXE) and its components
- Learn how to exploit the vulnerability
- Understand remediation measures

Important Concepts

**Extensible Markup Language (XML)**

XML is a commonly used method to transport and store data in a structured format that humans and machines can easily understand. Consider a scenario where two computers need to communicate and share data. Both devices need to agree on a common format for exchanging information. This agreement (format) is known as `XML`. You can think of XML as a digital filing cabinet. Just as a filing cabinet has folders with labelled documents inside, XML uses `tags` to label and organise information. These tags are like folders that define the type of data stored. This is what an XML looks like, a simple piece of text information organised in a structured manner: 

```javascript
<people>
   <name>Glitch</name>
   <address>Wareville</address>
   <email>glitch@wareville.com</email>
   <phone>111000</phone>
</people>
```

In this case, the tags **<people>**, **<name>**, **<address>**, etc are like folders in a filing cabinet, but now they store data about Glitch. The content inside the tags, like "`Glitch`," "`Wareville`," and "`123-4567`" represents the actual data being stored. Like before, the key benefit of XML is that it is easily shareable and customisable, allowing you to create your own tags. 

**Document Type Definition (DTD)**

Now that the two computers have agreed to share data in a common format, what about the structure of the format? Here is when the DTD comes into play. A DTD is a set of **rules** that defines the structure of an XML document. Just like a database scheme, it acts like a blueprint, telling you what elements (tags) and attributes are allowed in the XML file. Think of it as a guideline that ensures the XML document follows a specific structure.

For example, if we want to ensure that an XML document about `people` will always include a `name`, `address`, `email`, and `phone number`, we would define those rules through a DTD as shown below:  

```javascript
<!DOCTYPE people [
   <!ELEMENT people(name, address, email, phone)>
   <!ELEMENT name (#PCDATA)>
   <!ELEMENT address (#PCDATA)>
   <!ELEMENT email (#PCDATA)>
   <!ELEMENT phone (#PCDATA)>
]>
```

In the above DTD, **<!ELEMENT>**  defines the elements (tags) that are allowed, like name, address, email, and phone, whereas `#PCDATA` stands for parsed `people` data, meaning it will consist of just plain text.  

**Entities**

So far, both computers have agreed on the format, the structure of data, and the type of data they will share. Entities in XML are placeholders that allow the insertion of large chunks of data or referencing internal or external files. They assist in making the XML file easy to manage, especially when the same data is repeated multiple times. Entities can be defined internally within the XML document or externally, referencing data from an outside source. 

For example, an external entity references data from an external file or resource. In the following code, the entity `&ext;` could refer to an external file located at "`http://tryhackme.com/robots.txt`", which would be loaded into the XML, if allowed by the system:

```javascript
<!DOCTYPE people [
   <!ENTITY ext SYSTEM "http://tryhackme.com/robots.txt">
]>
<people>
   <name>Glitch</name>
   <address>&ext;</address>
   <email>glitch@wareville.com</email>
   <phone>111000</phone>
</people>
```

We are specifically discussing external entities because it is one of the main reasons that XXE is introduced if it is not properly managed.

**XML External Entity (XXE)**

After understanding XML and how entities work, we can now explore the XXE vulnerability. XXE is an attack that takes advantage of **how** **XML parsers handle external entities**. When a web application processes an XML file that contains an external entity, the parser attempts to load or execute whatever resource the entity points to. If necessary sanitisation is not in place, the attacker may point the entity to any malicious source/code causing the undesired behaviour of the web app.

For example, if a vulnerable XML parser processes this external entity definition:

```javascript
<!DOCTYPE people[
   <!ENTITY thmFile SYSTEM "file:///etc/passwd">
]>
<people>
   <name>Glitch</name>
   <address>&thmFile;</address>
   <email>glitch@wareville.com</email>
   <phone>111000</phone>
</people>
```

Here, the entity `&thmFile;` refers to the sensitive file `/etc/passwd` on a system. When the XML is processed, the parser will try to load and display the contents of that file, exposing sensitive information to the attacker.  

In the upcoming tasks, we will examine how XXE works and how to exploit it.

Connecting to the Machine

Before moving forward, review the questions in the connection card shown below: 

![Connetion card, AttackBox and Virtual Machine.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1731002645527.png)

Click on the green `Start Machine` button below to start the virtual machine. While the virtual machine starts, click on the **Start AttackBox** button at the top of the page and browse **Wareville's WishVille** application at `http://MACHINE_IP`. Please wait 1-2 minutes after the system boots completely to let the auto scripts run successfully.

Start Machine

Practical 

Now that you understand the basic concepts related to XML and XXE, we will analyse an application that allows users to view and add products to their carts and perform the checkout activity. You can access the Wareville application hosted on `http://MACHINE_IP`. This application allows users to request their Christmas wishes.

**Flow of the Application**  

As a penetration tester, it is important to first analyse the flow of the application. First, the user will browse through the products and add items of interest to their wishlist at `http://MACHINE_IP/product.php`. Click on the `Add to Wishlist` under `Wareville's Jolly Cap`, as shown below:

![Web application's product page.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1730813202090.png)  

After adding products to the wishlist, click the `Cart` button or visit `http://MACHINE_IP/cart.php` to see the products added to the cart. On the `Cart` page, click the `Proceed to Checkout` button to buy the items as shown below:

![Web application's cart details.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1730813300580.png)  

On the checkout page, the user will be prompted to enter his name and address as shown below:

![Web application's checkout details.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1730813382277.png)  

Enter any name of your choice and address, and click on `Complete Checkout` to place the wish. Once you complete the wish, you will be shown the message **"Wish successful. Your wish has been saved as Wish #21"**, as shown below:

![Wish #21 saved in a new file.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1730813503366.png)  

**Wish #21** indicates the wishes placed by a user on the website. Once you click on **Wish #21**, you will see a forbidden page because the details are only accessible to `admins`. But can we try to bypass this and access other people's wishes? This is what we will try to perform in this task.

![Error page when accessing the new wish page.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1730813503096.png)  

**Intercepting the Request**  

Before discussing exploiting XXE on the web, let's learn how to intercept the request. First, we need to configure the environment so that, as a pentester, all web traffic from our browser is routed through Burp Suite. This allows us to see and manipulate the requests as we browse. 

We will use Burp Suite, a powerful web vulnerability scanner, to intercept and modify requests for this exploitation. You can access Burp Suite in the `AttackBox`. On the desktop of the AttackBox, you will see a Burp Suite icon as shown below:

![Burp suite icon](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728456762740.png)  

Once you click the icon, Burp Suite will open with an introductory screen. You will see a message like "**Welcome to Burp Suite**". Click on the `Next` button. 

![Burp suite splash screen](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728457165300.png)  

On the next screen, you will have the option to `Start Burp`. Click on the `Start Burp` button to start the tool.

![Burp suite startup setting screen](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728457184817.png)  

Once Burp Suite has started, you will see its main interface with different tabs, such as `Proxy`, `Intruder`, `Repeater` and others.

![Burp suite dashboard with options](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728630460840.png)  

Inside Burp Suite, click the `Settings` tab at the top right. You will see Burp's browser option available under the `Tools` section. Enable `Allow Burp's browser to run without a sandbox option` and click on the **close icon** on the top right corner of the `Settings` tab as shown below:

![Enabling Burp browser settings](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728459438650.png)  

After allowing the browser to run without a sandbox, we would now be able to start the browser with pre-configured Burp Suite's proxy. Navigate to the `Open browser` option located at the `Proxy -> Intercept` section of Burp.  Open the browser by clicking the `Open browser` as shown below and browse the URL `http://MACHINE_IP`, so that all requests are intercepted: 

![opening browser with in Burp suite](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1728625481652.png)  

Once you browse the URL, all the requests are intercepted and can be seen under the `Proxy->HTTP history` tab.

![HTTP history tab of Burp.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1730813727577.png)  

**What is Happening in the Backend?**

Now, when you visit the URL, `http://MACHINE_IP/product.php`, and click `Add to Wishlist`, an AJAX call is made to `wishlist.php` with the following XML as input. 

```javascript
<wishlist>
  <user_id>1</user_id>
     <item>
       <product_id>1</product_id>
     </item>
</wishlist>
```

In the above XML, **<product_id>** tag contains the ID of the product, which is **1** in this case. Now, let's review the `Add to Wishlist` request logged in Burp Suite's `HTTP History` option under the proxy tab. As discussed above, the request contains XML being forwarded as a `POST` request, as shown below:

![View of the request sent to wishlist.php using Burp.](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1729006687410.png)  

This `wishlist.php` accepts the request and parses the request using the following code:

```javascript
<?php
..
...
libxml_disable_entity_loader(false);
$wishlist = simplexml_load_string($xml_data, "SimpleXMLElement", LIBXML_NOENT);

...
..
echo "Item added to your wishlist successfully.";
?>
```

**Preparing the Payload**

When a user sends specially crafted XML data to the application, the line `libxml_disable_entity_loader(false)` allows the XML parser to load external entities. This means the XML input can include external file references or requests to remote servers. When the XML is processed by `simplexml_load_string` with the `LIBXML_NOENT` option, the web app resolves external entities, allowing attackers access to sensitive files or allowing them to make unintended requests from the server.  

What if we update the XML request to include references for external entities? We will use the following XML instead of the above XML:

```javascript
<!--?xml version="1.0" ?-->
<!DOCTYPE foo [<!ENTITY payload SYSTEM "/etc/hosts"> ]>
<wishlist>
  <user_id>1</user_id>
     <item>
       <product_id>&payload;</product_id>
     </item>
</wishlist>
```

When we send this updated XML payload, the first two lines introduce an external entity called **payload**. The line <**!ENTITY payload SYSTEM "/etc/hosts">** tells the XML parser to replace the **&payload;** reference with the contents of the file **/etc/hosts** on the server. When the XML is processed, instead of a normal **product_id**, the application will try to load and include the contents of the file specified in the entity (`/etc/hosts`).

**Exploitation**

Now, let's perform the exploitation by repeating the request we captured earlier. The Burp Suite tool has a feature known as `Repeater` that allows you to send multiple HTTP requests. We will use this feature to duplicate our `HTTP POST` request and send it multiple times to exploit the vulnerability. Right-click on the `wishlist.php` POST request and click on `Send to Repeater`.  

![Instructions to send a request to the Repeater tab.](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1729012048433.png)

Now, switch to the `Repeater` tab, where you'll find the `POST` request that needs to be modified. We will update the XML payload with the new data as shown below and then send the modified request:

![Updated the XML with an XXE payload.](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1729018934528.png)  

Place the mouse cursor inside the request in the `Repeater` tab in Burp Suite and press `Ctrl+V`  or paste the payload in the above-highlighted area.

![Initial XXE payload and its response.](https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1729019108929.png)  

When we clicked `Send`, the server processed the malicious XML payload, which included the external entity reference to `/etc/hosts`. As a result, the `wishlist.php` responded with the contents of the `/etc/hosts` file, leading to an XXE vulnerability.

![Software playing with the web.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1730283613622.png)Time for Some Action

Now that you've identified a vulnerability in the application, it's time to see it in action! McSkidy Software has tasked us with finding loopholes, and we've successfully uncovered one in the `wishlist.php` endpoint. But our work doesn't end there—let's take it a step further and assess the potential impact this vulnerability could have on the application.

Earlier, we discovered a page accessible only by administrators, which seems like an exciting target. What if we could use the vulnerability we've found to access sensitive information, like the wishes placed by the townspeople?

Now that our objective is clear, let's leverage the vulnerability we discovered to read the contents of each wishes page and demonstrate the full extent of this flaw to help McSkidy secure the platform. To get started, let's recall the page that is only accessible by admins - `/wishes/wish_1.txt`. Using this path, we just need to guess the potential absolute path of the file. Typically, web applications are hosted on `/var/www/html`. With that in mind, let's build our new payload to read the wishes while leveraging the vulnerability.

**Note: Not all web applications use the path /var/www/html, but web servers typically use it.**

```javascript
<!--?xml version="1.0" ?-->
<!DOCTYPE foo [<!ENTITY payload SYSTEM "/var/www/html/wishes/wish_1.txt"> ]>
<wishlist>
	<user_id>1</user_id>
	<item>
	       <product_id>&payload;</product_id>
	</item>
</wishlist>
```

![Leaking the wishes via XXE.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1730814018118.png)  

Surprisingly, we got lucky that our assumption worked. The next thing to do is see whether we can view more wishes using our discovery. To do this, let's try replacing the `wish_1.txt` with `wish_2.txt`.

![Iterating within the wishes via XXE.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1730814073518.png)  

As a result, we were able to view the next wish. You may observe that we just incremented the number by one. Given this, you may continue checking the other wishes and see all the wishes stored in the application.

After iterating through the wishes, we have proved the potential impact of the vulnerability, and anyone who leverages this could read the wishes submitted by the townspeople of Wareville.

Conclusion

It was confirmed that the application was vulnerable, and the developers were not at fault since they only wanted to give the townspeople something before Christmas. However, it became evident that bypassing security testing led to an application that did not securely handle incoming requests.

As soon as the vulnerability was discovered, McSkidy promptly coordinated with the developers to implement the necessary mitigations. The following proactive approach helped to address the potential risks against XXE attacks:

- **Disable External Entity Loading**: The primary fix is to disable external entity loading in your XML parser. In PHP, for example, you can prevent XXE by setting `libxml_disable_entity_loader(true)` before processing the XML.
- **Validate and Sanitise User Input**: Always validate and sanitise the XML input received from users. This ensures that only expected data is processed, reducing the risk of malicious content being included in the request. For example, remove suspicious keywords like `/etc/host`, `/etc/passwd`, etc, from the request.

After discovering the vulnerability, McSkidy immediately remembered that a CHANGELOG file exists within the web application, stored at the following endpoint: [http://MACHINE_IP/CHANGELOG](http://machine_ip/CHANGELOG). After checking, it can be seen that someone pushed the vulnerable code within the application after Software's team.

![CHANGELOG data.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1729260978473.png)  

With this discovery, McSkidy still couldn't confirm whether the Mayor intentionally made the application vulnerable. However, the Mayor had already become suspicious, and McSkidy began to formulate theories about his possible involvement.

![Mayor Malware's schemes.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5dbea226085ab6182a2ee0f7/room-content/5dbea226085ab6182a2ee0f7-1730283636344.png)