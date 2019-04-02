# TCP-notifier
Server for sending notification to list of IPs

## Server side

Tcp notifier threads:
* Thread A listens for TCP connections. Thread is waiting for new IP addresses (in JSON form) or request to send data to groups.
* Thread B saves IP to HD/DB.
* Thread C loads IP list data from HD/DB and starts sending notifications to IPs.
* Thread D logs.

[[https://github.com/jurbbo/tcp-notifier/raw/master/images/notifer_server.png|alt=tcp_server_layout]]
