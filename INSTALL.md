## How to Install

The installer file:  ``getgrass.sh`` will source and download the extension, and place the files where they need to be on your system correctly.  You can run the following commands:

```
git clone https://github.com/loopyd/install-grass.git
cd install-grass
chmod +x ./getgrass.sh
sudo ./getgrass.sh install
```

> 🌱 **NEW FEATURE** The `-d` or ``--dry-run`` command-line argument will allow you to download, but not install the Grass Desktop node.  This is useful to see results of the installer, before you use it directly on your system.

On some distrobutions, installation of additional packages will be required.  The installer will prompt you which to search your package manager for, and install **manually**.  The names of the packages **may vary** based upon your distrobution.  You can access your package maintainer's resources to locate and install the nessecary packages.

## How to Update

The ``getgrass`` installer is run as the root user.  This means that permissions for manually installed files are owned by the root (UID=0, GID=0) user by default.  You will see the message "Update failed" in your Desktop Node when using ``getgrass`` while running in a non-root Window Manager session.  This is normal.  Extraction with ``ar`` via ``binutils`` is not able to preserve original ACLs, which is why this happens.

> 🌱 **NEW FEATURE** To correct this error, you can try the `-u` or ``-user-mode`` command line switch, which will make the files owned by your user instead of root.  This can sometimes fix update issues on systems where you don't desire to run a desktop session as root.

If all else fails, to update your node, close your Desktop Node by right-clicking and selecting "Quit" from your Window Manager's taskbar, then open a terminal and type:

```
sudo grass
```

Take the update when prompted.  When completed, close the Desktop Node in the same way again, and then open it from the Applications menu.  Your Grass Desktop Node will be on its most recent version!

## Help!  I have some Grass-GIS thingy, what do I do?

This is common on Ubuntu or Debian systems, as there's a conflicting project called grass that gets installed to a new version when your system gets updated.  On these systems, if you use **aptitude**, you can block the arbitrary and unassociated project with a **deprioritization pin**.

> 🌱 These instructions will differ for other package managers.  Please consult your package manager's documentation if you experience this conflict.  Searching its man pages for "blacklist" can help!

```sh
sudo apt-get remove grass* -y
echo "\nPackage: grass*\nPin: release c=universe\nPin-Priority: -100\n" | sudo tee -a /etc/apt/preferences.d/99-priority
```

Once you've done this, you'll need to run ``getgrass`` again.

```
./install.sh
```

Now when your system updates again, this shouldn't happen to you.

## Need more help?

You can add on the `-h` or ``-help`` command-line switch when invoking the installer utility to get further assistance, and some extra options!

We provide a [🔗 USAGE document](./USAGE.md) that details each available command line option.
