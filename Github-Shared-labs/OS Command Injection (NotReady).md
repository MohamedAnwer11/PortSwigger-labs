


## Lab: OS command injection, simple case

![](assets/Pasted%20image%2020251018054037.png)

![](assets/Pasted%20image%2020251018054126.png)

![](assets/Pasted%20image%2020251018054219.png)


![](assets/Pasted%20image%2020251018054300.png)

![](assets/Pasted%20image%2020251018054349.png)


---

## 2.Lab: Blind OS command injection with time delays

### Instructions:
This lab contains a blind OS command injection vulnerability in the feedback function.

The application executes a shell command containing the user-supplied details. The output from the command is not returned in the response.

To solve the lab, exploit the blind OS command injection vulnerability to cause a 10 second delay.

### Solution:


![](assets/Pasted%20image%2020251018062911.png)


![](assets/Pasted%20image%2020251018061859.png)

![](assets/Pasted%20image%2020251018062002.png)





![](assets/Pasted%20image%2020251018061708.png)



---

## 3. Lab: Blind OS command injection with output redirection

### Instructions:
This lab contains a blind OS command injection vulnerability in the feedback function.

The application executes a shell command containing the user-supplied details. The output from the command is not returned in the response. However, you can use output redirection to capture the output from the command. There is a writable folder at:
`/var/www/images/`
The application serves the images for the product catalog from this location. You can redirect the output from the injected command to a file in this folder, and then use the image loading URL to retrieve the contents of the file.

To solve the lab, execute the `whoami` command and retrieve the output.



### Solution:



![](assets/Pasted%20image%2020251019104010.png)

![](assets/Pasted%20image%2020251019103944.png)

![](assets/Pasted%20image%2020251019103856.png)



---

## Lab: Blind OS command injection with out-of-band interaction


**OAST (Out-of-Band Application Security Testing)** is a cybersecurity methodology used to detect vulnerabilities in web applications that do not produce immediate, visible responses—commonly known as _blind vulnerabilities_. Unlike traditional testing methods like SAST or DAST, OAST relies on external communication channels to confirm exploitation

### How OAST Works

OAST operates by injecting a payload into the target application that triggers an outbound network request (e.g., DNS or HTTP) to an **attacker-controlled or monitoring server**. If the server receives this callback, it confirms the presence of a vulnerability—even if no direct response is seen from the app

### Common OAST Techniques

1. **DNS-based OAST**: Most reliable, as DNS queries often bypass firewalls. Used to detect blind SSRF, RCE, or XSS.
    
2. **HTTP-based OAST**: Triggers HTTP requests to external servers; useful when outbound HTTP is allowed.
3. **Time-based OAST**: Infers vulnerabilities based on response delays, though less reliable than DNS callbacks
     
### Risks and Misuse

While OAST is a legitimate security testing technique, it's increasingly **weaponized by attackers**. Malicious packages in npm, PyPI, and RubyGems use OAST domains (e.g., `oast.fun`, `oastify.com`) for **stealthy data exfiltration** and **reconnaissance**, bypassing detection by mimicking benign DNS traffic
1. **Time-based OAST**: Infers vulnerabilities based on response delays, though less reliable than DNS callbacks




![](assets/Pasted%20image%2020251019105657.png)


![](assets/Pasted%20image%2020251019105147.png)

![](assets/Pasted%20image%2020251019105251.png)

![](assets/Pasted%20image%2020251019105400.png)



![](assets/Pasted%20image%2020251019105419.png)




----


## Blind OS command injection with out-of-band data exfiltration






![](assets/Pasted%20image%2020251019123414.png)

![](assets/Pasted%20image%2020251019123356.png)

![](assets/Pasted%20image%2020251019123316.png)

![](assets/Pasted%20image%2020251019123248.png)