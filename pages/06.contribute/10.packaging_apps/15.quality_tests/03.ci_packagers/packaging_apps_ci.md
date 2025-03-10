---
title: Continuous integration
template: docs
taxonomy:
    category: docs
routes:
  default: '/packaging_apps_ci'
---

The YunoHost project manages a [Continuous Integration Server](https://ci-apps-dev.yunohost.org/ci/) you can use to regularly test your integration.
It's running [package_check](https://github.com/YunoHost/package_check).

For this You need to have:
- Your repository transferred to [YunoHost-Apps repository](https://github.com/YunoHost-Apps)
- A clean check_process file in your repo [See syntax description here](https://github.com/YunoHost/package_check#syntax-of-check_process)
- It's recommended to have tested it locally before with [Package_check tool](https://github.com/YunoHost/package_check)

Thanks to a github bot, it's very easy to run a test:
- Just create a Pull Request in your github repo, and add the following comment: !testme
- You should then be greeted almost immediatly by a comment from the bot like this
![image](https://user-images.githubusercontent.com/771800/211145536-6f84c5f4-5172-4498-83cb-9acd5b96ba21.png)
- Sometimes the bot is not being triggered... Just smile and try again !
- Then clicking on this comment will go to the Continuous Integration Server with your status of test

The test will be scheduled in a queue, once it is run and complete, the following will happen:
- The bot will add the result in the PR as a new comment
- Your README in the repository will be updated with the test result and the updated integration level of your application.

At any time you can have a look at [the CI Server homepage](https://ci-apps-dev.yunohost.org/ci/) to see what tests are currently ongoing.

! The rest of this page is outdated and should be reworked

A continuous integration server is available for any packager willing to test an app with [Package_check](https://github.com/YunoHost/package_check).

[ci-apps-dev](https://ci-apps-dev.yunohost.org?classes=btn,btn-lg,btn-primary)

This server is free to use for any of you, you just need an account.  
To do so, ask to a member of the Apps group on our [Applications chatroom](/chat_rooms)

To create an account on this CI, you'll need two things:
- A name (To create an user and to give it a directory).
- A public ssh key (For your access to the server).

When that's done, you'll be able to access the server and put your apps on it.  
To connect to the server use:
```bash
ssh USER@ci-apps-dev.yunohost.org -i YOUR_PRIVATE_KEY
```

You will find an empty directory, ready to receive your apps.  
As soon as you push an app into your directory, in a 5 minutes maximum delay, a new job will be created for this app and executed by the CI.  
Each time you will update this app, a new test will be executed.

However, to prevent any security issues, your ssh connection will be very limited.  
You can only use `sftp` or `rsync` to copy your apps into that directory. `Git` isn't available, neither most of the usual bash commands.  
To ease your usage of this CI, a small script can be used to copy your apps to your directory.

Copy this [script](https://raw.githubusercontent.com/YunoHost/CI_package_check/master/dev_CI/send_to_dev_ci.sh) into your usual working directory and fill it with your info.

Make sure the content of your `check_process` file is correct then transfer your files.
When your files have been transfered, you can monitor the CI pipeline on https://ci-apps-dev.yunohost.org.

---

# Other continuous integration servers

For your information, here the list of all our continuous integration servers.  
Those CI are automatic, you can't use them directly. They're working on their own.

- [Official CI](https://ci-apps.yunohost.org): Our official CI, working on a x86-64 system. It is in charge of determining levels for all working apps.
- [ARM CI](https://ci-apps-arm.yunohost.org): This CI is working with multiple Raspberry-Pi, own by members of the YunoHost community. Tests are running on Raspberry-Pi to determine if apps are working on this architecture.
- [Unstable/Testing CI](https://ci-apps-unstable.yunohost.org): CI designed to run tests on the branches Unstable and Testing of YunoHost. Its purpose is to test those branches before an official release.
- [Jessie CI](https://ci-stretch.nohost.me): CI running on a Debian Jessie system. This CI determine is apps are still working with the previous version of Debian and YunoHost before the version 3.
- [HQ CI](https://ci-apps-hq.yunohost.org): **Incoming...** This CI runs automatic tests on branches of High Quality apps. Except the master branch, which is exclude from this CI, all branches added to a High Quality app will be added to this CI to be tested.
