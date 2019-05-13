![](https://img.shields.io/badge/Ansible-tomcat-green.svg?logo=angular&style=for-the-badge)

>__Please note that the original design goal of this role was more concerned with the initial installation and bootstrapping environment, which currently does not involve performing continuous maintenance, and therefore are only suitable for testing and development purposes,  should not be used in production environments.__

>__请注意，此角色的最初设计目标更关注初始安装和引导环境，目前不涉及执行连续维护，因此仅适用于测试和开发目的，不应在生产环境中使用。__
___

<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/logo_tomcat.png" align="right" /></p>

__Table of Contents__

- [Overview](#overview)
- [Requirements](#requirements)
  * [Operating systems](#operating-systems)
  * [Tomcat Versions](#tomcat-versions)
- [ Role variables](#Role-variables)
  * [Minimal Configuration](#minimal-configuration)
  * [Main Configuration](#Main-parameters)
  * [Other Configuration](#Other-parameters)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Hosts inventory file](#Hosts-inventory-file)
  * [Vars in role configuration](#vars-in-role-configuration)
  * [Combination of group vars and playbook](#combination-of-group-vars-and-playbook)
- [License](#license)
- [Author Information](#author-information)
- [Contributors](#Contributors)

## Overview
This Ansible role installs  apache tomcat on linux operating system, including establishing a filesystem structure and server configuration with some common operational features.

## Requirements
### Operating systems
This role will work on the following operating systems:

  * CentOS 6,7

### Apache Tomcat versions

The following list of supported the tomcat releases:

* Apache Tomcat 8.0, 8.5

## Role variables
### Main parameters #
There are some variables in defaults/main.yml which can (Or needs to) be overridden:

#### General parameters
* `tomcat_version` should contain the Apache Tomcat releases version.
* `tomcat_selinux`: SELinux policy.
* `java_home`: Environment variable to point to an installed JDK.
* `system_service`: Path for system service file.
* `syslog`:  A boolean value,  Enable or Disable console and access log to remote syslog server.
* `syslog_server`: IP address of syslog server.
* `syslog_port`: Port of syslog server.

##### Service Mesh
* `environments`: Define the service environment.
* `consul_public_register`: Whether register a exporter service with public consul client.
* `consul_public_exporter_token`: Public Consul client ACL token.
* `consul_public_clients`: List of public consul clients.
* `consul_public_http_port`: The consul HTTP API port.

#### Listen port
* `tomcat_port.http_connectors`: The TCP port number of HTTP connectors.
* `tomcat_port.https_connectors`: The TCP port number on HTTPs connectors.
* `tomcat_port.jmx_port`: Prometheus jmx_exporter port .
* `tomcat_port.rmi_port`: The port to be used by the JMX/RMI registry for the Platform server.
* `tomcat_port.server_port`: Tomcat Server port.
* `tomcat_port.wrapper`: A socket to communicate with its Java component running inside a JVM.
* `tomcat_port.wrapper_jvm`: A socket to communicate with its Java component running inside a JVM.

#### System Variables
* `tomcat_arg.cookie_protect`: Set-Cookie HttpOnly & Secure response header.
* `tomcat_arg.disable_ipv6`: Deny IPv6 socket connect If IPv6 is available on the operating system.
* `tomcat_arg.jmxremote`: Enabling JMX Remote function.
* `tomcat_arg.jvm_heapdumppath`: Heap dump folder.
* `tomcat_arg.jvm_security_egd`: Random number generation library.
* `tomcat_arg.jvm_xss`:Thread stack size.
* `tomcat_arg.lc_ctype`: The language of messages.
* `tomcat_arg.minimumUmask`:The least restrictive umask for Security Lifecycle Listener.
* `tomcat_arg.path`: Specify the Tomcat working directory.
* `tomcat_arg.rmi_gcInterval`:RMI Forces periodic full collection interval in minutes.
* `tomcat_arg.session_timeout`: Tomcat Session Timeout.
* `tomcat_arg.sslciphersuite`: The SSL Ciphers.
* `tomcat_arg.sslprotocol`: The SSL protocols.
* `tomcat_arg.timezone`: Default timezone for a single instance of a running JVM.
* `tomcat_arg.uid`: System user ID for running tomcat services.
* `tomcat_arg.ulimit_core`: The number of core dump launched by systemd.
* `tomcat_arg.ulimit_nofile`: The number of files launched by systemd.
* `tomcat_arg.ulimit_nproc`: The number of processes launched by systemd.
* `tomcat_arg.user`: System user name for running tomcat services.
* `tomcat_arg.web_protect`: Includeing Force SSL / Disable ETag / Allow-Methods / HSTS.
* `tomcat_arg.wrapper_console_format`: Format to use for output to the console.
* `tomcat_arg.wrapper_console_loglevel`: Log level to use for console output.
* `tomcat_arg.wrapper_java_command_loglevel`: Log level to use for Java command.
* `tomcat_arg.wrapper_logfile`: Sets the path to the Wrapper log file.
* `tomcat_arg.wrapper_logfile_format`: Format to use for logging to the log file.
* `tomcat_arg.wrapper_logfile_loglevel`: Filters messages sent to the log file according to their log levels.
* `tomcat_arg.wrapper_logfile_maxfiles`: Controls the maximum number of rolled files.
* `tomcat_arg.wrapper_logfile_maxsize`:  Controls the maximum size of rolled files.
* `tomcat_arg.wrapper_syslog_loglevel`: Log level to use for logging to the Event Log on syslog on UNIX systems.
* `tomcat_arg.wrapper_ulimit_loglevel`: Controls at which log level resource limits will be logged.

### Other parameters
There are some variables in vars/main.yml:

## Dependencies
There are no dependencies on other roles.

## Example

### Hosts inventory file
See tests/inventory for an example.

    node01 ansible_host='192.168.1.10' tomcat_version='8.0.53'
    node02 ansible_host='192.168.1.11' tomcat_version='8.0.53'
    node03 ansible_host='192.168.1.12' tomcat_version='8.0.53'

### Vars in role configuration
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - role: ansible-role-linux-tomcat
           tomcat_version: '8.0.53'

### Combination of group vars and playbook
You can also use the group_vars or the host_vars files for setting the variables needed for this role. File you should change: group_vars/all or host_vars/`group_name`

    tomcat_selinux: false
    java_home: '/usr/lib/jvm/java'
    system_service: '/lib/systemd/system'
    syslog: true
    syslog_server: '1.1.1.1'
    syslog_port: '12209'
    tomcat_port:
      http_connectors: '8080'
      https_connectors: '8443'
      jmx_port: '9404'
      rmi_port: '10201-10202'
      server_port: '8005'
      wrapper: '31000-31999'
      wrapper_jvm: '32000-32999'
    tomcat_arg:
      cookie_protect: true
      disable_ipv6: true
      jmxremote: true
      jvm_heapdumppath: '/tmp'
      jvm_security_egd: '/dev/urandom'
      jvm_xss: '256k'
      lc_ctype: 'zh_CN.UTF-8'
      minimumUmask: '0007'
      path: '/data/tomcat'
      rmi_gcInterval: '28800'
      session_timeout: '10'
      sslciphersuite: 'ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256'
      sslprotocol: 'TLSv1+TLSv1.1+TLSv1.2'
      timezone: 'Asia/Shanghai'
      uid: '2001'
      ulimit_core: 'unlimited'
      ulimit_nofile: '10240'
      ulimit_nproc: '10240'
      user: 'tomcat'
      web_protect: true
      wrapper_console_format: 'PM'
      wrapper_console_loglevel: 'INFO'
      wrapper_java_command_loglevel: 'NONE'
      wrapper_logfile: 'catalina.out'
      wrapper_logfile_format: 'TM'
      wrapper_logfile_loglevel: 'INFO'
      wrapper_logfile_maxfiles: '25'
      wrapper_logfile_maxsize: '50m'
      wrapper_syslog_loglevel: 'NONE'
      wrapper_ulimit_loglevel: 'STATUS'
    environments: 'SIT'
    consul_public_register: false
    consul_public_exporter_token: '00000000-0000-0000-0000-000000000000'
    consul_public_clients: 'localhost'
    consul_public_http_port: '8500'

## License

![](https://img.shields.io/badge/MIT-purple.svg?style=for-the-badge)

## Author Information
Please send your suggestions to make this role better.

## Contributors
Special thanks to the [Connext Information Technology](http://www.connext.com.cn) for their contributions to this role.
