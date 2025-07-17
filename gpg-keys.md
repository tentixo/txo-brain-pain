# GPG Keys 
## This document explains what are GPG keys, describes steps for creation of GPG keys and how are they different from SSH keys.  

### GPG Key Use Cases
- Digitally sign Git commits to prove authorship
- Encrypt and decrypt files for secure communication
- Email encryption (used in PGP, Pretty Good Privacy)

### Creation of GPG keys

Generate GPG key  by opening terminal and following the steps: 
1. Generate  
```
gpg --full-generate-key
```
2. You will be prompted with following  
![](img/GPG_KindofKey.jpg)
3. Set the key size  
![](img/GPG_KeySize.jpg)
4. Enter key validity, be careful for how long you would want it to be valid.  Below is an example -
![](img/GPG_KeyValidity.jpg)
5. GnuPG needs to construct a user ID to identify your key.

Real name:  
_Name must be at least 5 characters long_  
Email address: <put email used to login to github>  
Comment: none  
6. Your process of key creation should be completed in above step.  Example output after key creation:
``` 
/Users/yourname/.gnupg/pubring.kbx
---------------------------------
sec   rsa4096/1234ABCD5678EFGH 2024-02-15 [SC]
      ABCD1234EFGH5678IJKL9012MNOP3456QRST7890
uid           [ultimate] Your Name <your-email@example.com>
ssb   rsa4096/5678IJKL9012MNOP 2024-02-15 [E] 
```
Where
- sec (Secret Key) → Your primary private key
- rsa4096/1234ABCD5678EFGH (SC) → The key ID used for signing (S) and certification (C)  
- 5678IJKL9012MNOP [E] → A subkey used for encryption (E) (not needed for GitHub)

### Add the GPG Key to GitHub
1. Export the Public Key  
Run this command with the correct key ID (refer example above) (1234ABCD5678EFGH from your output)  
``` gpg --armor --export 1234ABCD5678EFGH ```
2. Copy the output, which will look like this  
```
-----BEGIN PGP PUBLIC KEY BLOCK-----
...
-----END PGP PUBLIC KEY BLOCK-----
```
3. Add the Key to GitHub  
   1. Add the key to GitHub → Settings → SSH and GPG keys
   2. Click “New GPG Key”
   3. Paste the exported key
   4. Click “Add GPG Key”

### Activating GPG key  
1. List your keys using ```gpg --list-secret-keys --keyid-format=long```  
2. Look for the line with [SC] (Signing & Certification)  
  _Example output_  
      sec   rsa4096/1234ABCD5678EFGH 2024-02-15 [SC]  
      ABCD1234EFGH5678IJKL9012MNOP3456QRST7890  
      uid           [ultimate] Your Name <your-email@example.com>  
3. Tell Git to Use Your GPG Key  
```
git config --global user.signingkey 1234ABCD5678EFGH
git config --global commit.gpgsign true
git config --global gpg.program $(which gpg)
```
4. Check If GPG Signing is Enabled in Git  
  
```
git config --global --list | grep gpg
```
   Expected output:  
   ` 
   commit.gpgsign=true  
   user.signingkey=1234ABCD5678EFGH  
   gpg.program=/opt/homebrew/bin/gpg
   `
### Error Handling
#### “gpg: cannot open ‘/dev/tty’: Device not configured” in Git Commit on macOS  
The error indicates that GPG is unable to prompt for your passphrase, which prevents Git from signing commits. This usually happens in GUI-based tools like PyCharm or VS Code, where there’s no direct terminal (/dev/tty) for GPG to interact with.  
Follow as under -   
1. Enable pinentry-mac (GUI Passphrase Prompt)  
Since PyCharm does not provide a terminal for GPG, configure GPG to use a graphical passphrase prompt.  
    1. Ensure pinentry-mac is Installed  
    ```
    which pinentry-mac
    ```
    expected output - `/opt/homebrew/bin/pinentry-mac`  
    2. If not installed, install it using Homebrew -   
    ```
    brew install pinentry-mac
    ```
2. Configure GPG to Use pinentry-mac  
```
echo "use-agent" >> ~/.gnupg/gpg.conf
echo "pinentry-program /opt/homebrew/bin/pinentry-mac" >> ~/.gnupg/gpg-agent.conf
echo "allow-loopback-pinentry" >> ~/.gnupg/gpg-agent.conf
gpgconf --kill gpg-agent  # Restart GPG agent
gpgconf --launch gpg-agent
```
Now, GPG should prompt for your passphrase in a popup window instead of the terminal.  
3. Manually Cache Your GPG Passphrase  
If pinentry-mac is set up correctly, but Git still fails to sign, you can manually cache your passphrase so that PyCharm doesn’t need to ask every time.  
```
echo "test" | gpg --sign --armor
```
If a popup appears, enter your passphrase.  
Note: GPG caches your passphrase only for a limited time. Default-cache -→ Your passphrase is cached for 10 minutes.  
__That’s why the cache expires after a certain period.__

### Key Differences - GPG and SSH
| **Feature**         | **GPG Key (GNU Privacy Guard)**                   | **SSH Key (Secure Shell)**                                    |
|---------------------|---------------------------------------------------|---------------------------------------------------------------|
| **Purpose**         | Encrypt/sign files, emails, Git commits           | Authenticate with remote servers, GitHub, etc.                |
| **Encryption**      | Uses asymmetric encryption (public/private keys)  | Uses public-key authentication for secure access              |
| **Use Case**        | Sign Git commits, encrypt emails, verify software | Log in to remote servers, authenticate GitHub, automate CI/CD |
| **GitHub Usage**    | Signs commits for verified authorship             | Allows passwordless authentication for Git operations         |
| **Example Command** | `gpg --sign`                                      | `ssh -T git@github.com`                                       |

GitHub can use both GPG and SSH keys together when signing and authenticating commits.  However, they serve different purposes -  
- GPG Key - Signs commits to verify the author’s identity (commit signing)
- SSH Key - Authenticates Git operations (e.g., git push, git fetch) without requiring a password

