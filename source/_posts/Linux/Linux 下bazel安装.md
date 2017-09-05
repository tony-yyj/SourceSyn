---
title: Linux 下bazel安装
tags:
  - Linux
  - Tensorflow
categories: Linux
date: 2017-09-05 20:18:00
---

<!-- toc -->
<!-- more -->

[Installing Bazel on Ubuntu - Bazel](https://docs.bazel.build/versions/master/install-ubuntu.html)
Install using binary installer

The binary installers are on Bazel's GitHub releases page.

The installer contains the Bazel binary and the required JDK. Some additional libraries must also be installed for Bazel to work.

1. Install required packages

sudo apt-get install pkg-config zip g++ zlib1g-dev unzip python
2. Download Bazel

Go to Bazel's GitHub releases page.[https://github.com/bazelbuild/bazel/releases](https://github.com/bazelbuild/bazel/releases)

Download the binary installer bazel-0.5.2-installer-linux-x86_64.sh. This installer contains the Bazel binary and the required JDK, and can be used even if JDK is already installed.

Note that bazel-0.5.2-without-jdk-installer-linux-x86_64.sh also exist. It is a version without embedded JDK 8. Only use this installer if you already have JDK 8 installed.

3. Run the installer

Run the installer:

chmod +x bazel-0.5.2-installer-linux-x86_64.sh
./bazel-0.5.2-installer-linux-x86_64.sh --user
The --user flag installs Bazel to the $HOME/bin directory on your system and sets the .bazelrc path to $HOME/.bazelrc. Use the --help command to see additional installation options.

4. Set up your environment

If you ran the Bazel installer with the --user flag as above, the Bazel executable is installed in your $HOME/bin directory. It's a good idea to add this directory to your default paths, as follows:

export PATH="$PATH:$HOME/bin"
You can also add this command to your ~/.bashrc file.