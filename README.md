Role Name
=========

Ansible role that installs Android SDK.

Requirements
------------
**The following tools must be installed on the target machine in order to proceed**

`unzip` Required to unzip the archive with Android SDK command line tools

`java`  Required to run `sdkmanager`

Role Variables
--------------

```yaml
android_sdk_location: /usr/local/android/sdk
commandline_tools_link: https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip
android_dependencies:
  - "build-tools;35.0.0"
  - "platforms;android-34"
  - "cmdline-tools;latest"
  - "emulator"
  - "extras;google;m2repository"
  - "tools"
  - "system-images;android-34;google_apis;x86_64"
```

`android_sdk_location` The location where Android SDK will be installed

`commandline_tools_link` A link to the Android SDK command line tools (can be found at https://developer.android.com/studio#command-line-tools-only)

`android_dependencies` A list of Android SDK dependencies that needs to be installed. A full list of dependencies can be obtained using `sdkmanager --list`

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      become: true
      roles:
         - android-sdk

License
-------
Apache License 2.0
