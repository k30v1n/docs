# How to add SSH to github

## Linux / macOS
First run the following query

```
ssh-keygen -t ed25519 -C "your_email@example.com"
```

This creates a new SSH key, using the provided email as a label.

When you're prompted to "Enter a file in which to save the key," press Enter. This accepts the default file location.

At the prompt, type a secure passphrase.    

Before adding a new SSH key to the ssh-agent to manage your keys, you should have checked for existing SSH keys and generated a new SSH key. 

```
eval "$(ssh-agent -s)"
```

Add your SSH private key to the ssh-agent. If you created your key with a different name, or if you are adding an existing key that has a different name, replace id_ed25519 in the command with the name of your private key file.

```
ssh-add ~/.ssh/id_ed25519
```

Then print the SSH public key on console
```
cat ~/.ssh/id_ed25519.pub
```

Copy and paste this value on Github profile on SSH.