* Here in patching we have to block the `AES CBC bit flipping attack`.
* For that checking the cookie[:32] is best thing >> `assert cookie[:32] == iv.encode('hex')`.Because for AES CBC attack is not possible without changing the cookie's first part.
------------------
* Without AES CBC attck the attacker has to give 'admin' string directly.
* So we modify the `assert username != 'admin'` to `assert username[:5] != 'admin'`
* Like this we can prevent the username from being a 'admin'.
* Without `username == 'admin'` . The `role=admin'` injection doesn't make any sense.
* So No need to look at role injection
#### Patched File :: [encrypt.py](https://github.com/Ajay-Aj-00/Test/blob/master/patch/encrypt.py)
