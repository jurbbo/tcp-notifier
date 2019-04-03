# TCP-notifier
TCP-notifier contains 3 different code snippets. Server code for sending notification to list of IPs. Client script code for making notification push requests and client application code for sending IP's and for listening to notifications.

## Server architecture

Tcp notifier threads:
* Thread A listens to TCP connections. Thread is waiting for new IP addresses (in JSON form) or request to send data to groups.
* Thread B saves IP to HD/DB.
* Thread C loads IP list data from HD/DB and starts sending notifications to IPs.
* Thread D logs.

![](https://github.com/jurbbo/tcp-notifier/raw/master/images/notifier_server.png)

### Different thread solutions

* Every new TCP-connection could start a new thread. Probably easier to code.
* Reader thread could set response-jobs to queue and one worker thread could work with the queue.

Since server can listen and send data simultaniously, concurrency enables minimun packet loss.

## Client architecture

For the application there are 2 different clients:
* Script calls server for a notification push. 
* Application sends own IP to server (to server's IP list) and listens to notification pushes.

Client's architecture, considering threads, is simplier than server. Client doesn't need to send and receive same time. Program that uses notification data, needs one listener thread. Push notification will be sent to server from script where concurrancy is not needed.

![](https://github.com/jurbbo/tcp-notifier/raw/master/images/client_server.png)
