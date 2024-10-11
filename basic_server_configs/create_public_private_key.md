# Create a public-private key pair for SSH to use with GitHub

## 1. Check if you already have SSH keys set up:
   ```
   ls -al ~/.ssh
   ```
   If you see files like `id_rsa.pub` or `id_ed25510.pub`, you might already have an SSH key. If not, you can create one.

## 2. Generate a new SSH key
   You can generate a new SSH key using the `ssh-keygen` command:
   ```
   ssh-keygen -t ecdsa -b 521
   ```
- `-t ecdsa` especifies the type of key.
- `-b 521` is the size of the key.

  If your system doesn't support `ecdsa`, use
  ```
  ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
  ```

  After running the command:

- When prompted to "Enter a file in which to save the key," you can press Enter to use the default location (`~/.ssh/id_ed25519` or `~/.ssh/id_rsa`).
- Optionally, add a passphrase for extra security, or just press Enter for no passphrase.


## 3. Add your SSH key to the SSH agent

Start SSH agent
```
eval "$(ssh-agent -s)"
```

Then add your SSH private key to the SSH agent
```
ssh-add ~/.ssh/id_ecdsa
```
(Replace `id_ecdsa` with the name of your key file if different.)

## 4. Add the SSH key to your GitHub account

You need to add your public key (not the private key) to GitHub.

- Copy the public key to your clipboard:
  ```
  cat ~/.ssh/id_ecdsa.pub
  ```
  Copy the entire output.
- Go to your [GitHub SSH settings](https://github.com/settings/keys) and click "New SSH key".
- Paste the key into the "Key" field, and give it a title.
- Click "Add SSH key".


## 5. Test your SSH connection
Finally, test your SSH connection to GitHub:
```
ssh -T git@github.com
```

If everything is set up correctly, you will see a success message similar to:
```
Hi username! You've successfully authenticated, but Github does not provide shell access.
```
