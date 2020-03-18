# git


## Establish SSH authentication 
When working with a GitHub repository, you'll often need to identify yourself to GitHub using your username and password. An SSH key is an alternate way to identify yourself that doesn't require you to enter you username and password every time.

SSH keys come in pairs, a public key that gets shared with services like GitHub, and a private key that is stored only on your computer. If the keys match, you're granted access.

The cryptography behind SSH keys ensures that no one can reverse engineer your private key from the public one.

### 1. Check for existing SSH keys
Run this command:
```bash
ls -al ~/.ssh
```
**If nothing is listed, then follow with step 2.**
If you see a file called `id_rsa.pub`, then you can **skip step 2.**

### 2. Generate a SSH-Key
Run
```bash
ssh-keygen -o -t rsa -C "YOUR@EMAIL.COM"
```
to generate a new key. **I recommend you to use the email adress you used to create your GitHub account here.**
You will be asked something like
```bash
Enter passphrase (empty for no passphrase):
```
which is actually a password you can set (and I recommend you doing so) to protect the key (Please remember the password/passphrase in the session 😉).

A quick check with
```bash
ls -al ~/.ssh
```
should now list `id_rsa.pub` among other items.

### 3. Add your public key to GitHub
Run
```bash
cat ~/.ssh/id_rsa.pub
```
which will print the Key to your console. Mark all of it and copy it (by pressing CMD+C).

Now we need to give out key to GitHub. That takes place here: https://github.com/settings/keys (This link might ask you to login first). Click the **"New SSH key"** button and you will see the following:
![alt text](https://help.github.com/assets/images/help/settings/ssh-key-paste.png "Add new SSH key")

In the "Title" field, add a descriptive label for the new key. For example, if you're using a personal Mac, you might call this key "Personal MacBook Air".

Paste your key into the "Key" field (by CMD+V).

Click **"Add SSH key"** button and confirm with your GitHub password (not the passphrase you might just have set).

### 4. Test if everything worked out well
Run
```bash
ssh -T git@github.com
```
and check whether there is something like
```bash
> The authenticity of host 'github.com (IP ADDRESS)' can't be established.
  > RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
  > Are you sure you want to continue connecting (yes/no)?
```
or
```bash
> The authenticity of host 'github.com (IP ADDRESS)' can't be established.
  > RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
  > Are you sure you want to continue connecting (yes/no)?
```

If so, then type `yes` and then hopefully you see something like
```bash
> Hi <USERNAME>! You've successfully authenticated, but GitHub does not
> provide shell access.
```
Verify that the resulting message contains your username, of course.
Then all is set up perfectly 😎
