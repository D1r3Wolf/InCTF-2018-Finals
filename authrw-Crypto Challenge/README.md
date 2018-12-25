# authrw
* [authrw](https://github.com/Ajay-Aj-00/Test/tree/master/authrw) is a **Crypto Challenge** given in InCTF-2018 Finals Attack and Defence
* It uses the `AES 128-bit CBC mode Encrytion`.`IV(16 bytes)` is given in iv.txt but we have to **generate the key** using [generate_key.py](https://github.com/Ajay-Aj-00/Test/tree/master/authrw/generate_key.py) which takes the Team password as input.The generated Key is `md5 hash of Team password`.
* **It Runs a Crypto Service in which it has `Login` and `Register` services**
![Login,Register](https://raw.githubusercontent.com/Ajay-Aj-00/Test/master/Images/1.png "Service")
### 1 - Register
* For the Register it asks the user for **username** (username != 'admin')
* Then it Encrypts the `pad("username=input():role=ordinary")` with AES CBC 128-bit Encryption
* After that It returns a cookie which is `"IV+Cipher_text".encode('hex')`
![Register](https://raw.githubusercontent.com/Ajay-Aj-00/Test/master/Images/R.png "Register")
> Analyze the cookie
 ![Register](https://raw.githubusercontent.com/Ajay-Aj-00/Test/master/Images/S.png "Register")
### 2 - Login
* For the Login it asks for cookie(Provided after registration)
* Then It Decrypts it , unpad it >> `username=(username):role=ordinary` and It parses the string and saves username and role in user , role variables
> After All these There are Three conditions to check the `user,role values`<br>
> 1 `user=='admin' and role=='ordinary'`<br>
> 2 `user=='admin' and role=='admin'`<br>
> 3 `else condition:`<br>
* Here Comes the Problem We cant give the 'admin' as username while registering Then we cant get user as 'admin' after decryption so we move to else condition.
* But they have some Vullnerabilities. See the Below links(`Exploiting the Vulnerabilities`)
> In Those 3 conditions<br>
> 1 Provides us Reading rights of Flag([Reading authorization](https://github.com/Ajay-Aj-00/Test/tree/master/authR_Exploit))<br>
> 2 Provides us Writing rights of Flag([Writing authorization](https://github.com/Ajay-Aj-00/Test/tree/master/authW_Exploit))<br>
## Now the name `authrw` is making sense `authrization for Reading and Writing`<br>
* Defending our services is also important. So we have to [patch](https://github.com/Ajay-Aj-00/Test/tree/master/patch) the Vulnerabilities.
