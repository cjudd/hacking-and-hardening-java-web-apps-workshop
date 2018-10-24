# Setup

During setup, you will install a [Kali Linux](https://www.kali.org/) virtual machine. Kali Linux is a flavor of linux intentinally designed for penetration testers.

## Requirements

- [VirtualBox](https://www.virtualbox.org/)
- [Workshop virtual machine](https://s3.amazonaws.com/cmj-presentations/hacking-uberconf-2016/hhjwa-2016.1-vbox-amd64.ova) - This is a version of [Kali Linux](https://www.kali.org/) with an intentinally vulnerable app called [Wordy Ninja Blog](https://github.com/cjudd/wordyninjablog) and a couple other penetration testing applications.

## Setup Virtual Machine

1. Install and start VirtualBox.

2. Download virtual machine.

3. Import virtual machine hhjwa-2016.1-vbox-amd64.ova using File > Import Appliance.

4. Run the Kali-Linux-2016.1-vbox-amd64 machine.

5. When prompted for username and password use root/toor.

NOTE: One of the things I like most about Kali Linux is how the Applications menu is organized for the different types of tasks a penetration tester would be involved in.

## Run Wordy Ninja Blog

1. Open a terminal.

2. Change directory to the application directory.

```
cd ~/workspaces/wordyninjablog
```

3. Get a specific version (a version that already has all the maven dependencies cached on the virtual machine) of the code.

```
git fetch && git checkout a74b32f
```

4. Run Wordy Ninja Blog.

```
./gradlew run
```

## Test the application

1. Open the Iceweasel browser (version of Firefox).

2. Navigate to [http://localhost:8080](http://localhost:8080).

3. Login as either admin/admin1234 or blogger1/blogger1234 and add some new posts.