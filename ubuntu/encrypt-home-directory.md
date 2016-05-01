# Encrypt Home Directory

(Ubuntu 14.04)

If you want to encrypt a home directory for existing users run:

```bash
sudo apt-get install ecryptfs-utils cryptsetup
```

Login as admin user (must be a different user than the user which home directory you want to encrypt).

The following command will take some time. **After the command has been executed, it's important that you login as the user which home folder has been encrypted** ***before the next reboot!***

```bash
sudo ecryptfs-migrate-home -u [username]
```

**Logout and login as `[username]`.**

After login, a dialog "Record your encryption passphrase" will be displayed after a while.

Click on "Run this action now" and enter your login password at the "Passphrase" prompt. Save the generated passphrase in a password manager.

To print the passphrase run `ecryptfs-unwrap-passphrase` and enter the password.

#### Clean up

Restart the system and check if you're able to login and everything works properly. You can then remove the backup home folder in `/home/[username].[random_id]`.

#### Revert encryption

In case you are not able to access your home directory anymore you can revert the encryption by using the backup in `/home/[username].[random_id]`.

Login as an admin user and rename or remove the current `/home/[username]` directory.

Then rename the `/home/[username].[random_id]` to `/home/[username]`.

You also need to remove the directory `/home/.ecryptfs/[username]`.

After a restart you should be able to login to your unencrypted account.

#### Resources

This TIL is based on http://www.howtogeek.com/116032/how-to-encrypt-your-home-folder-after-installing-ubuntu/.

For more info about eCryptfs, available tools and how to use them check http://ecryptfs.org/documentation.html.
