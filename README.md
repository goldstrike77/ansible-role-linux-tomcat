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
* `tomcat_java_home`: Environment variable to point to an installed JDK.
* `tomcat_path`: Specify the Tomcat working directory.
* `tomcat_jmxremote`: Enabling JMX Remote function.
* `tomcat_web_protect`: Includeing Force SSL / Disable ETag / Allow-Methods / HSTS.
* `tomcat_cookie_protect`: Set-Cookie HttpOnly & Secure response header.
* `tomcat_disable_ipv6`: Deny IPv6 socket connect If IPv6 is available on the operating system

#### JVM memory Variables
* `tomcat_jvm_metaspace`: Size of the metaspace in MB.
* `tomcat_jvm_xmn`: Size of the heap for the young generation in MB.
* `tomcat_jvm_xmx`: Size of the heap in MB.
* `tomcat_jvm_xss`: Size of thread stack.

##### Service Mesh
* `environments`: Define the service environment.
* `tags`: Define the service custom label.
* `exporter_is_install`: Whether to install prometheus exporter.
* `consul_public_register`: false Whether register a exporter service with public consul client.
* `consul_public_exporter_token`: Public Consul client ACL token.
* `consul_public_clients`: List of public consul clients.
* `consul_public_http_port`: The consul HTTP API port.

##### Syslog parameters
* `syslog`: A boolean value,  Enable or Disable send console and access log to remote Syslog server.
* `syslog_port`: Syslog server port.
* `syslog_protocol`: Syslog server protocol.
* `syslog_server`: List of syslog server list.

#### Listen port
* `tomcat_port_http`: The TCP port number of HTTP connectors.
* `tomcat_port_https`: The TCP port number on HTTPs connectors.
* `tomcat_port_jmx`: Prometheus jmx_exporter port .
* `tomcat_port_rmi`: The port to be used by the JMX/RMI registry for the Platform server.
* `tomcat_port_server`: Tomcat Server port.
* `tomcat_port_wrapper`: A socket to communicate with its Java component running inside a JVM.
* `tomcat_port_wrapper_jvm`: A socket to communicate with its Java component running inside a JVM.

#### System Variables
* `tomcat_arg.jvm_heapdumppath`: Heap dump folder.
* `tomcat_arg.jvm_security_egd`: Random number generation library.
* `tomcat_arg.lc_ctype`: The language of messages.
* `tomcat_arg.minimumUmask`:The least restrictive umask for Security Lifecycle Listener.
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

    tomcat_version: '8.0.53'
    tomcat_java_home: '/usr/lib/jvm/java'
    tomcat_path: '/data'
    tomcat_jmxremote: true
    tomcat_web_protect: true
    tomcat_cookie_protect: true
    tomcat_disable_ipv6: true
    tomcat_port_http: '8080'
    tomcat_port_https: '8443'
    tomcat_port_jmx: '9404'
    tomcat_port_rmi: '10201-10202'
    tomcat_port_server: '8005'
    tomcat_port_wrapper: '31000-31999'
    tomcat_port_wrapper_jvm: '32000-32999'
    tomcat_jvm_metaspace: '256'
    tomcat_jvm_xmn: '128'
    tomcat_jvm_xmx: '1024'
    tomcat_jvm_xss: '256'
    tomcat_arg:
      jvm_heapdumppath: '/tmp'
      jvm_security_egd: '/dev/urandom'
      lc_ctype: 'zh_CN.UTF-8'
      minimumUmask: '0007'
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
    syslog: false
    syslog_port: '12201'
    syslog_protocol: 'udp'
    syslog_server:
      - '127.0.0.1'
    environments: 'SIT'
    tags:
      subscription: 'default'
      owner: 'nobody'
      department: 'Infrastructure'
      organization: 'The Company'
      region: 'IDC01'
    exporter_is_install: false
    consul_public_register: false
    consul_public_exporter_token: '00000000-0000-0000-0000-000000000000'
    consul_public_http_port: '8500'
    consul_public_clients:
      - '127.0.0.1'

## License

![](https://img.shields.io/badge/MIT-purple.svg?style=for-the-badge)

## Author Information
Please send your suggestions to make this role better.

## Contributors
Special thanks to the [Connext Information Technology](http://www.connext.com.cn) for their contributions to this role.
