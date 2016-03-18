# ansible-haproxy

[haproxy](http://www.haproxy.org/) - The Reliable, High Performance TCP/HTTP Load Balancer

[![Platforms](http://img.shields.io/badge/platforms-ubuntu-lightgrey.svg?style=flat)](#)
[![Status](https://travis-ci.org/telusdigital/ansible-haproxy.svg?branch=master)](#)

Tunables
--------
* `haproxy_version` (integer) - Version number of haproxy to install
* `haproxy_user` (string) - User to run haproxy as
* `haproxy_group` (string) - Group to run haproxy as
* `haproxy_error_handling_enabled` (boolean) - Handle errors?
* `haproxy_attack_mitigation_enabled` (boolean) - Aggressively favour resiliency over compatibility?
* `haproxy_assumes_backend_is_dead_after` (integer) - If a backend has not accepted the connection in this long, it's probably dead.
* `haproxy_runtime_root` (string) - Directory for runtime data
* `haproxy_pidfile_path` (string) - Path for pidfile
* `haproxy_stats_socket_path` (string) - Path for socket
* `haproxy_chroot_path` (string) - Directory haproxy should sandbox itself into
* `haproxy_standard_configuration` (boolean) - Use the config generators?
* `haproxy_autodeploy_passthrough_enabled` (boolean) - Allow passthrough for automated deployment
* `haproxy_stats_enabled` (boolean) - Enable stats
* `haproxy_stats_uri` (string) - Context path for stats UI
* `haproxy_stats_user` (string) - Username for stats
* `haproxy_stats_password` (string) - Password for stats
* `haproxy_protocol` (string) - Protocol to use
* `haproxy_ssl_enabled` (boolean) - Enable SSL handling?
* `haproxy_ssl_certificate_path` (string) - Path to SSL certificate
* `haproxy_ssl_ciphers` (list) - Ranked set of acceptable ciphers
* `haproxy_ssl_should_degrade_security_to_accomodate_old_browsers` (boolean) - Compromise security to support older browsers?
* `haproxy_ssl_redirect_http_to_https` (boolean) - Redirect HTTP to HTTPS
* `haproxy_ssl_disable_sslv3` (boolean) - Disable SSLv3
* `haproxy_perfect_forward_secrecy_enabled` (boolean) - Enable PFS?
* `haproxy_load_balancer_enabled` (boolean) - Adjust backend names to accomodate ELBs from telusdigital.infrastructure
* `haproxy_standard_application` (boolean) - Is this a typical application?
* `haproxy_backend_name` (string) - Name for the backend.
* `haproxy_backend_server_port` (integer) - Port for backend.
* `haproxy_frontend_port` (integer) - Port for frontend.
* `haproxy_backend_server_direct`: "application{% if haproxy_load_balancer_enabled %}-direct{% endif %}.{{ * `project` }}-{{ environment_tier }}.{{ domain }}{% if haproxy_ssl_enabled %}:{{ haproxy_backend_server_* `port` }}{% endif %}"
* `haproxy_backend_server_load_balancer`: "application.{{ project }}-{{ environment_tier }}.{{ domain }}{% * `if` haproxy_ssl_enabled %}:{{ haproxy_backend_server_port }}{% endif %}"
* `haproxy_backend_host_range_enabled` (boolean) - Use a range of IPs
* `haproxy_backend_network` (string) - First three octets of a IP range
* `haproxy_backend_host_range_start` (integer) - Beginning of range
* `haproxy_backend_host_range_end` (integer) - End of range
* `haproxy_restricted_paths` (list) - Paths to restrict access to
* `haproxy_allow_access_to_restricted_paths_from_ips` (list) - IPs to allow access to restricted paths
* `haproxy_tune_ssl_default_dh_param` (integer) - Sets the maximum size of the Diffie-Hellman parameters used for generating the ephemeral/temporary Diffie-Hellman key

Dependencies
------------
* [telusdigital.apt-repository](https://github.com/telusdigital/ansible-apt-repository/)

Example Playbook
----------------
    - hosts: servers
      roles:
         - role: telusdigital.haproxy
           haproxy_backend_host_range_enabled: yes
           haproxy_backend_network: 10.0.2
           haproxy_backend_host_range_start: 20
           haproxy_backend_host_range_end: 40

License
-------
[MIT](https://tldrlegal.com/license/mit-license)

Contributors
------------
* [Chris Olstrom](https://colstrom.github.io/) | [e-mail](mailto:chris@olstrom.com) | [Twitter](https://twitter.com/ChrisOlstrom)
* Steven Harradine
* Aaron Pederson
* Ben Visser
