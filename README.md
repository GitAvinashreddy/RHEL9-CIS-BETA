# RHEL 9 CIS

## Configure a RHEL 9 machine to be [CIS](https://www.cisecurity.org/cis-benchmarks/) compliant

### Based on [ CIS RedHat Enterprise Linux 9 Benchmark v1.0.0 - 11-30-2022 ](https://www.cisecurity.org/cis-benchmarks/)

---

![Org Stars](https://img.shields.io/github/stars/ansible-lockdown?label=Org%20Stars&style=social)
![Stars](https://img.shields.io/github/stars/ansible-lockdown/RHEL9-CIS?label=Repo%20Stars&style=social)
![Forks](https://img.shields.io/github/forks/ansible-lockdown/RHEL9-CIS?style=social)
![followers](https://img.shields.io/github/followers/ansible-lockdown?style=social)
[![Twitter URL](https://img.shields.io/twitter/url/https/twitter.com/AnsibleLockdown.svg?style=social&label=Follow%20%40AnsibleLockdown)](https://twitter.com/AnsibleLockdown)

![Ansible Galaxy Quality](https://img.shields.io/ansible/quality/61781?label=Quality&&logo=ansible)
![Discord Badge](https://img.shields.io/discord/925818806838919229?logo=discord)

![Devel Build Status](https://img.shields.io/github/actions/workflow/status/ansible-lockdown/RHEL9-CIS/linux_benchmark_testing.yml?label=Devel%20Build%20Status)
![Devel Commits](https://img.shields.io/github/commit-activity/m/ansible-lockdown/RHEL9-CIS/devel?color=dark%20green&label=Devel%20Branch%20commits)

![Release Branch](https://img.shields.io/badge/Release%20Branch-Main-brightgreen) 
![Main Build Status](https://img.shields.io/github/actions/workflow/status/ansible-lockdown/RHEL9-CIS/linux_benchmark_testing.yml?label=Build%20Status)
![Main Release Date](https://img.shields.io/github/release-date/ansible-lockdown/RHEL9-CIS?label=Release%20Date)
![Release Tag](https://img.shields.io/github/v/tag/ansible-lockdown/RHEL9-CIS?label=Release%20Tag&&color=success)

![Issues Open](https://img.shields.io/github/issues-raw/ansible-lockdown/RHEL9-CIS?label=Open%20Issues)
![Issues Closed](https://img.shields.io/github/issues-closed-raw/ansible-lockdown/RHEL9-CIS?label=Closed%20Issues&&color=success)
![Pull Requests](https://img.shields.io/github/issues-pr/ansible-lockdown/RHEL9-CIS?label=Pull%20Requests)

![License](https://img.shields.io/github/license/ansible-lockdown/RHEL9-CIS?label=License)

---

## Looking for support?

[Lockdown Enterprise](https://www.lockdownenterprise.com#GH_AL_RH9_cis)

[Ansible support](https://www.mindpointgroup.com/cybersecurity-products/ansible-counselor#GH_AL_RH9_cis)

### Community

Join us on our [Discord Server](https://discord.io/ansible-lockdown) to ask questions, discuss features, or just chat with other Ansible-Lockdown users.

---

## Caution(s)

This role **will make changes to the system** which may have unintended consequences. This is not an auditing tool but rather a remediation tool to be used after an audit has been conducted.

Check Mode is not supported! The role will complete in check mode without errors, but it is not supported and should be used with caution. The RHEL8-CIS-Audit role or a compliance scanner should be used for compliance checking over check mode.

This role was developed against a clean install of the Operating System. If you are implementing to an existing system please review this role for any site specific changes that are needed.

To use release version please point to main branch and relevant release for the cis benchmark you wish to work with.

---

## Matching a security Level for CIS

It is possible to to only run level 1 or level 2 controls for CIS.
This is managed using tags:

- level1_server
- level1_workstation
- level2_server
- level2_workstation

The control found in defaults main also need to reflect this as this control the testing thet takes place if you are using the audit component.

## Coming from a previous release

CIS release always contains changes, it is highly recommended to review the new references and available variables. This have changed significantly since ansible-lockdown initial release.
This is now compatible with python3 if it is found to be the default interpreter. This does come with pre-requisites which it configures the system accordingly.

Further details can be seen in the [Changelog](./ChangeLog.md)

## Auditing (new)

This can be turned on or off within the defaults/main.yml file with the variable rhel8cis_run_audit. The value is false by default, please refer to the wiki for more details. The defaults file also populates the goss checks to check only the controls that have been enabled in the ansible role.

This is a much quicker, very lightweight, checking (where possible) config compliance and live/running settings.

A new form of auditing has been developed, by using a small (12MB) go binary called [goss](https://github.com/goss-org/goss) along with the relevant configurations to check. Without the need for infrastructure or other tooling.
This audit will not only check the config has the correct setting but aims to capture if it is running with that configuration also trying to remove [false positives](https://www.mindpointgroup.com/blog/is-compliance-scanning-still-relevant/) in the process.

Refer to [RHEL9-CIS-Audit](https://github.com/ansible-lockdown/RHEL9-CIS-Audit).

## Documentation

- [Read The Docs](https://ansible-lockdown.readthedocs.io/en/latest/)
- [Getting Started](https://www.lockdownenterprise.com/docs/getting-started-with-lockdown#GH_AL_RH9_cis)
- [Customizing Roles](https://www.lockdownenterprise.com/docs/customizing-lockdown-enterprise#GH_AL_RH9_cis)
- [Per-Host Configuration](https://www.lockdownenterprise.com/docs/per-host-lockdown-enterprise-configuration#GH_AL_RH9_cis)
- [Getting the Most Out of the Role](https://www.lockdownenterprise.com/docs/get-the-most-out-of-lockdown-enterprise#GH_AL_RH9_cis)

## Requirements

RHEL 9
Almalinux 9
Rocky 9
OracleLinux 9

ansible 2.10
jmespath
relevant collections

- Access to download or add the goss binary and content to the system if using auditing (other options are available on how to get the content to the system.)

**General:**

- Basic knowledge of Ansible, below are some links to the Ansible documentation to help get started if you are unfamiliar with Ansible

  - [Main Ansible documentation page](https://docs.ansible.com)
  - [Ansible Getting Started](https://docs.ansible.com/ansible/latest/user_guide/intro_getting_started.html)
  - [Tower User Guide](https://docs.ansible.com/ansible-tower/latest/html/userguide/index.html)
  - [Ansible Community Info](https://docs.ansible.com/ansible/latest/community/index.html)
- Functioning Ansible and/or Tower Installed, configured, and running. This includes all of the base Ansible/Tower configurations, needed packages installed, and infrastructure setup.
- Please read through the tasks in this role to gain an understanding of what each control is doing. Some of the tasks are disruptive and can have unintended consiquences in a live production system. Also familiarize yourself with the variables in the defaults/main.yml file.

**Technical Dependencies:**

- Python3
- Ansible 2.9+
- python-def (should be included in RHEL 9)
- libselinux-python
- pip packages
  - jmespath ( complete list found in requirements.txt)
- collections found in collections/requirememnts.yml

## Role Variables

This role is designed that the end user should not have to edit the tasks themselves. All customizing should be done by overriding the required varaibles as found in defaults/main.yml file. e.g. using inventory, group_vars, extra_vars

## Tags

There are many tags available for added control precision. Each control has it's own set of tags noting what level, if it's scored/notscored, what OS element it relates to, if it's a patch or audit, and the rule number.

Below is an example of the tag section from a control within this role. Using this example if you set your run to skip all controls with the tag services, this task will be skipped. The opposite can also happen where you run only controls tagged with services.

```sh
      tags:
      - level1-server
      - level1-workstation
      - scored
      - avahi
      - services
      - patch
      - rule_2.2.4
```

## Community Contribution

We encourage you (the community) to contribute to this role. Please read the rules below.

- Your work is done in your own individual branch. Make sure to Signed-off and GPG sign all commits you intend to merge.
- All community Pull Requests are pulled into the devel branch
- Pull Requests into devel will confirm your commits have a GPG signature, Signed-off, and a functional test before being approved
- Once your changes are merged and a more detailed review is complete, an authorized member will merge your changes into the main branch for a new release

## Known Issues

CIS 1.2.4 - repo_gpgcheck is not carried out for RedHat hosts as the  default repos do not have this function. This also affect EPEL(not covered by var).
          - Rocky and Alma not affected.
Variable used to unset.
rhel9cis_rhel_default_repo: true  # to be set to false if using repo that does have this ability

## Pipeline Testing

uses:

- ansible-core 2.12
- ansible collections - pulls in the latest version based on requirements file
- runs the audit using the devel branch
- This is an automated test that occurs on pull requests into devel

## Local Testing

ansible-base 2.10.17 - python 3.8
ansible-core 2.13.4  - python 3.10

- makefile - this is there purely for testing and initial setup purposes.
































## v1.0.0 - released Dec 2022

![Build Status](https://img.shields.io/github/workflow/status/ansible-lockdown/RHEL9-CIS/CommunityToDevel?label=Devel%20Build%20Status&style=plastic)
![Build Status](https://img.shields.io/github/workflow/status/ansible-lockdown/RHEL9-CIS/DevelToMain?label=Main%20Build%20Status&style=plastic)
![Release](https://img.shields.io/github/v/release/ansible-lockdown/RHEL9-CIS?style=plastic)



## Join us

On our [Discord Server](https://discord.io/ansible-lockdown) to ask questions, discuss features, or just chat with other Ansible-Lockdown users

## Caution(s)

This role **will make changes to the system** which may have unintended concequences.

This role was developed against a clean install of the Operating System. If you are implimenting to an existing system please review this role for any site specific changes that are needed.

To use release version please point to main branch

## Documentation

- [Readthedocs](https://ansible-lockdown.readthedocs.io/en/latest/)
- [Getting Started](https://www.lockdownenterprise.com/docs/getting-started-with-lockdown)
- [Customizing Roles](https://www.lockdownenterprise.com/docs/customizing-lockdown-enterprise)
- [Per-Host Configuration](https://www.lockdownenterprise.com/docs/per-host-lockdown-enterprise-configuration)
- [Getting the Most Out of the Role](https://www.lockdownenterprise.com/docs/get-the-most-out-of-lockdown-enterprise)

## Requirements

RHEL 9
Almalinux 9
Rocky 9
OracleLinux 9

ansible 2.10
jmespath
relevant collections

- Access to download or add the goss binary and content to the system if using auditing (other options are available on how to get the content to the system.)

## Tested with

ansible-base 2.10.17 - python 3.8
ansible-core 2.13.4  - python 3.10

- makefile - this is there purely for testing and initial setup purposes.

## General

- Basic knowledge of Ansible, below are some links to the Ansible documentation to help get started if you are unfamiliar with Ansible
  - [Main Ansible documentation page](https://docs.ansible.com)
  - [Ansible Getting Started](https://docs.ansible.com/ansible/latest/user_guide/intro_getting_started.html)
  - [Tower User Guide](https://docs.ansible.com/ansible-tower/latest/html/userguide/index.html)
  - [Ansible Community Info](https://docs.ansible.com/ansible/latest/community/index.html)

- Functioning Ansible and/or Tower Installed, configured, and running. This includes all of the base Ansible/Tower configurations, needed packages installed, and infrastructure setup.
- Please read through the tasks in this role to gain an understanding of what each control is doing.
  - Some of the tasks are disruptive and can have unintended consiquences in a live production system. Also familiarize yourself with the variables in the defaults/main.yml file

## Dependencies

- Python3
- Ansible 2.9+
- python-def (should be included in RHEL 9)
- libselinux-python
- pip packages
  - jmespath ( complete list found in requirements.txt)
- collections found in collections/requirememnts.yml





### Known Issues

CIS 1.2.4 - repo_gpgcheck is not carried out for RedHat hosts as the  default repos do not have this function. This also affect EPEL(not covered by var).
          - Rocky and Alma not affected.
Variable used to unset.
rhel9cis_rhel_default_repo: true  # to be set to false if using repo that does have this ability
