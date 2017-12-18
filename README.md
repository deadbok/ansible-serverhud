# Ansible role to install server hud

## Compatibility

 * Debian 9 (stretchs)

## Variables

### Service configuration

 * **serverhud_install_server** (*yes/no*): Enable the server hud server
 * **serverhud_install_client** (*yes/no*): Enable the server hud client
 * **serverhud_server_service** (*string*): server hud server service name (default: serverhud-server)
 * **serverhud_client_service** (*string*): server hud client service name (default: serverhud-server)

### User and path

 * **serverhud_user** (*string*): User that runs the server hud service (default: serverhud)
 * **serverhud_group** (*string*): Group that runs the server hud service (default: serverhud)
 * **serverhud_home_dir** (*string*): Path to the home directory of the user running server hud (default: /opt/serverhud)

### Package, logs, and configuration locations

  * **serverhud_pip_uri** (*string*): Server hud pip package URI to install from (default: git+https://github.com/deadbok/server-hud)
  * **serverhud_config_path** (*string*): Base directory of the service configuration file (default: {{ serverhud_home_dir }})
  * **serverhud_server_config_path** (*string*): Path to the configuration file of the server (default: {{ serverhud_config_path }}/serverhud-server-config.py)
  * **serverhud_client_config_path** (*string*): Path to the configuration file of the server (default: {{ serverhud_config_path }}/serverhud-client-config.py).
  * **serverhud_log_path** (*string*): Path to the log directory of the service (default: {{ serverhud_home_dir }})

## States of packages and services

 * **serverhud_state** (*started/stopped*): Initial state of the server hud service after installation (default: started)
 * **serverhud_restart_state** (*restarted/reloaded*) The state of the server hud service after a configuration change (default: restarted).
 * **serverhud_packagess_state** (*installed/latest*) Whether to make sure the latest server hud packages are installed (default: latest)

## Server and client configuration

The following values are written to the server hud configuration files. They
are special they are Python files, and so the values given here should be correct Python syntax.

### General

 * **serverhud_debug** (*True/False*) Whether to enable debug logging (default: False)
 * **serverhud_allowed** (*list of strings*) List of hosts that are allowed to access this service (default: [getfqdn() + ':5000', gethostname() + ':5000', 'localhost:5000'])

### Client

 * **serverhud_client_host** (*dictionary of panel -> hostname mappings*) Dictionary of hosts to fetch data for the panels from. Currently the list of visible panels is hardcoded. (default: {'web_connections': 'localhost:5000', 'web_remote_host': 'localhost:5000', 'web_uptime': 'localhost:5000', 'web_accesses': 'localhost:5000', 'fw_connections': 'localhost:5000', 'fw_speed': 'localhost:5000'})

### Server

 * **serverhud_server_process** (*string*) Process to use when calculating uptime. (default: lighttd)
 * **serverhud_server_access_log** (*string*) Access log of the web server. (default: /var/log/lighttpd/access.log)
 * **serverhud_server_interface** (*string*) Network interface to use when calculating speed. (default: eth1)
 * **serverhud_server_ports** (*list of strings*) Port to scan for number of connections. (default: 80)
 * **serverhud_server_services** (*list of strings*) List of enabled services on the server. (default: [])
