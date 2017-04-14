# sample_role_oracle-java

A sample [Ansible](http://www.ansible.com) role to setup Oracle Java Development Kit. 

DISCLAIMER: usage of any version of this role implies you have accepted the
[Oracle Binary Code License Agreement for Java SE](http://www.oracle.com/technetwork/java/javase/terms/license/index.html).


## Requirements

- ansible >= 1.8.4


# Facts
|        variable               |                               description                                                   |   
|:-----------------------------:|:-------------------------------------------------------------------------------------------:|
| oracle_java_installed         | fact set by this role that contains a flag that indicates if Java is installed on the host. |
| oracle_java_version_installed | fact set by this role that contains the string of the Java version installed in the system. |


## Role Variables

|              variable             | default | description |
|:---------------------------------:|:------------:|:-----------------------------------------------------------------------------------------------------------|
| oracle_java_set_as_default        |    no   | make the newly installed Java the default runtime environment.                                                  |
| oracle_java_state                 | latest  | the package state (see Ansible apt module for more information).                                                |
| oracle_java_version               |    8    | the Oracle JDK version to be installed.                                                                         |
| oracle_java_version_update        |    45   | the Oracle JDK version update.                                                                                  |
| oracle_java_version_build         |   14    | the Oracle JDK version update build number.                                                                     |
| oracle_java_version_string        | 1.{{ oracle_java_version }}.0_u{{ oracle_java_version_update }} | the Java version string to verify installation against. |
| oracle_java_os_supported variable |    -    | role internal variable to check if a OS family is supported or not.                                             | 


### Debian-only

| variable | default | description |
|:--------------------------------------:|:------:|:-------------------------------------------------------------------------------------|
| launchpad_ppa_webupd8_cache_valid_time | 3600   | the amount of time in seconds the apt cache is valid.                                |
| oracle_java_cache_valid_time           | 3600   | the amount of time in seconds the apt cache is valid.                                |
| oracle_java_state                      | latest | the package state (see Ansible apt module for more information).                     |
| oracle_java_home                       | /usr/lib/jvm/java-{{ oracle_java_version }}-oracle | the location of the Java home directory. |


### Redhat-only

| variable | default | description |
|:-:|:-:|:--|
| oracle_java_dir_source | /usr/local/src | directory where to store RPMs (Redhat-only). |
| oracle_java_home | /usr/java/jdk1.{{ oracle_java_version }}.0_{{ oracle_java_version_update }} | the location of the Java home directory. |
| oracle_java_rpm_filename | jdk-{{ oracle_java_version }}u{{ oracle_java_version_update }}-linux-x64.rpm | the filename of the RPM. |
| oracle_java_rpm_url | http://download.oracle.com/otn-pub/java/jdk/{{ oracle_java_version }}u{{ oracle_java_version_update }}-b{{ oracle_java_version_build }}/{{ oracle_java_rpm_filename }} | the URL where the RPM can be downloaded from. |


## Dependencies

For Debian and Ubuntu this role depends on:

- sample_role_launchpad-ppa-webupd8


## Playbooks

    - hosts: servers
      roles:
         - { role: sample_role_oracle-java,
             oracle_java_set_as_default: yes }

Use `--skip-tags=debug` if you want to suppress debug information.


## Author Information

