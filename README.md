Ansible Android SDK Role
=========

Ansible role that installs minimal Android SDK (command line tools).

Requirements
------------
**The following tools must be installed on the target machine in order to proceed**

`unzip` Required to unzip the archive with Android SDK command line tools

Role Variables
--------------

```yaml
android_cmdline_temp_dir: "/tmp/cmdlinetools"
android_sdk_location: /usr/local/android/sdk
commandline_tools_link: https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip
```

`android_cmdline_temp_dir` Initial directory where Android command line tools will be installed. After installing, the
`{{ android_cmdline_temp_dir }}/cmdline-tools/` directory is moved to `{{ android_sdk_location }}/cmdline-tools/latest`
directory.

`android_sdk_location` The location where Android SDK will be installed.

`commandline_tools_link` A link to the Android SDK command line tools (can be found
at https://developer.android.com/studio#command-line-tools-only)

Dependencies
------------

None

Example Playbook
----------------
The role installs only Android command line tools. After the tasks in role have been played, the `sdkmanager`
tool will be available which may be used to install Android SDK components. The recommended way is to use `android_sdk`
task
from [`community.general`](https://docs.ansible.com/ansible/devel/collections/community/general/android_sdk_module.html)
collection (version >=10.2.0)

    - hosts: servers
      become: true
      roles:
         - shamilovstas/ansible-android-role
      tasks:
      - name: Install java
        apt:
          name: openjdk-17-jre-headless
          state: present
  
      - name: Install build-tools
        environment:
          PATH: "{{ ansible_env.PATH }}:{{ android_sdk_location }}/cmdline-tools/latest/bin"
        community.general.android_sdk:
          name: build-tools;34.0.0
          state: present
          accept_licenses: true

License
-------
Apache License 2.0