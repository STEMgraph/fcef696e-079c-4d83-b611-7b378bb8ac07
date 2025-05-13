<!---
{
  "id": "fcef696e-079c-4d83-b611-7b378bb8ac07"
  "depends_on": ["AND", "d58d972d-7730-4b1c-8ec2-a8288ef0ed05", "7f50ba23-f5a6-4bc7-887f-ed9247220544"],
  "author": "Exercise Sheet Assistant",
  "first_used": "2025-05-13",
  "keywords": ["apt", "dpkg", "linux", "package management", "command line"]
}
--->


# Introduction to the `apt` Package Manager

> In this exercise you will learn how to use the `apt` package manager to install, manage, and remove software on Debian-based Linux systems. Furthermore we will explore how `apt` compares to other package management systems and understand the underlying principles of software installation on Unix-like systems.

### Introduction

Package managers are fundamental tools in modern Linux systems. They automate the process of installing, upgrading, configuring, and removing software packages, along with handling their dependencies. `apt`, short for Advanced Package Tool, is the default front-end for package management on Debian and its derivatives, including Ubuntu.

`apt` builds upon `dpkg`, the lower-level Debian package management tool. While `dpkg` can install `.deb` files and query the local package database, it does not resolve dependencies automatically. `apt`, on the other hand, communicates with online repositories, downloads necessary files, and ensures all dependencies are met. This makes `apt` more user-friendly and suitable for everyday package management tasks.

A *repository* in this context is a collection of software packages stored on a remote server. These repositories are curated by maintainers and provide secure, up-to-date software that can be easily retrieved and installed by package managers.

Why don't we install software manually, say by downloading and compiling source code? The answer lies in convenience, security, and consistency. Package managers ensure you get trusted, verified software tailored for your system. They maintain records, allow upgrades, and remove software cleanly without leaving orphaned files.

Installing software means more than copying files. It involves placing them in correct directories, setting permissions, updating menus or paths, and registering with system databases. Unmanaged installations lack these safeguards, leading to potential conflicts and security risks.

Beyond `apt` and `dpkg`, other popular package managers include `yum` and `dnf` for RPM-based distributions, `pacman` for Arch Linux, and `zypper` for openSUSE. Each has unique features but serves the same core purpose.

### Further Readings and Other Sources

* [Debian Wiki on APT](https://wiki.debian.org/Apt)
* [APT vs DPKG Explained - YouTube](https://www.youtube.com/watch?v=57Ra2c7AvtE)
* [APT documentation (manpages)](https://man7.org/linux/man-pages/man8/apt.8.html)

## Tasks

### Task 1: Install the `sl` Package

1. Open your terminal.
2. Update your package list:

   ```sh
   sudo apt update
   ```
3. Install the `sl` package:

   ```sh
   sudo apt install sl
   ```
4. Run `sl` by typing:

   ```sh
   sl
   ```

   This playful command simulates a steam locomotive — try it out!

### Task 2: Add Another Repository

In Linux systems, repositories are centralized servers where collections of software packages are stored and maintained. These repositories are essential for a secure and efficient software installation process. Ubuntu includes several default repositories, such as 'main' and 'restricted', which are maintained by Canonical. The 'universe' repository, however, contains community-maintained software. While not officially supported, it greatly expands the available software. Adding a repository makes its contents available for installation and upgrades via the package manager.

1. Attempt to install a package from the "universe" repository:

   ```sh
   sudo apt install byobu
   ```

   This will likely fail because the repository is not enabled yet.
2. Edit your sources list using `vim`:

   ```sh
   sudo vim /etc/apt/sources.list
   ```
3. Add the following line:

   ```
   deb http://archive.ubuntu.com/ubuntu focal universe
   ```
4. Save and exit `vim`, then update:

   ```sh
   sudo apt update
   ```
5. Retry installing the package:

   ```sh
   sudo apt install byobu
   ```

   It should now succeed, as the package is available in the added repository.

### Task 3: Add a Key to the Keychain and Install a Third-Party Package

Linux package repositories use cryptographic signatures to ensure the authenticity and integrity of their packages. These signatures are verified using GPG keys. If the key is not available on your system, apt will reject the package source. Therefore, before installing software from an external repository, it is essential to add the corresponding GPG key to your system’s trusted keyring.

1. Try installing a third-party package not found in default repositories:

   ```sh
   sudo apt install neofetch
   ```

   This will fail because the repository and key are not yet configured.
2. Create a new file for the repository using `vim`:

   ```sh
   sudo vim /etc/apt/sources.list.d/neofetch.list
   ```
3. Add the following line:

   ```
   deb http://ppa.launchpad.net/dawidd0811/neofetch/ubuntu focal main
   ```
4. Save and exit `vim`.
5. Add the GPG key for the repository:

   ```sh
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3B4FE6ACC0B21F32
   ```
6. Update your package list:

   ```sh
   sudo apt update
   ```
7. Try installing again:

   ```sh
   sudo apt install neofetch
   ```

   It should now work, as the repository and key have been added correctly.

### Task 4: Upgrade Installed Packages

1. To see available upgrades:

   ```sh
   apt list --upgradable
   ```
2. To upgrade all packages:

   ```sh
   sudo apt upgrade
   ```

   Upgrading means replacing currently installed packages with newer versions, which often includes security patches, bug fixes, and new features.

### Task 5: Uninstall a Package

1. Remove `sl` without deleting configuration files:

   ```sh
   sudo apt remove sl
   ```

   This uninstalls the program but keeps config files for potential reuse. Keeping config files is useful if you plan to reinstall the software with previous settings intact.

### Task 6: Purge Packages Completely

1. To remove the package and its configuration files:

   ```sh
   sudo apt purge sl
   ```
2. Also purge `byobu` and `neofetch` to remove them completely:

   ```sh
   sudo apt purge byobu neofetch
   ```

   This ensures a cleaner uninstallation with no trace left behind, which is useful when completely resetting or eliminating a package.

## Questions

1. What are the main differences between `apt` and `dpkg`?
2. Why is using a package manager safer than manual installation?
3. What does the `apt update` command do?
4. How do you add a new software source in Debian-based systems?
5. What is the purpose of adding a GPG key when adding a repository?
6. What is the difference between `apt remove` and `apt purge`?

## Advice

Learning to manage packages using `apt` is a fundamental skill for anyone working with Debian-based systems. It saves time, ensures security, and helps you keep your system in a maintainable state. As you proceed, try exploring advanced topics like pinning packages, holding versions, or using `aptitude`. Mastering these tools will make you a more effective and self-sufficient Linux user. Don't hesitate to revisit related exercises like \[UUID-dpkg-basic-001] or \[UUID-apt-troubleshooting-002] once you're comfortable with the basics.
