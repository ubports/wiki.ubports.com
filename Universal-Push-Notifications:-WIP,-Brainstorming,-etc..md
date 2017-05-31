## Motivation ##
Currently there is no open, universal push infrastructure existing on this planet that will allow independent OS projects to push messages between (mobile) devices. The goal is to provide first a concept that would make such a infrastructure possible. It should be hosted on distributed servers, maintained by individuals or organizations.

## Participants ##
Currently the following groups of people showed interest:

 * Sailfish OS developers
 * UBports developers
 
## Cornerstones ##
 The service shall be:
 
  * Lightweight
  * Cross-Platform
  * Distributed
  * Clustered
  * Pluggable for various authentication schemes of clients & servers
  * Manageable to restrict abuse
  
## Current status ##
### SFOS ###
  * SFOS has currently no working push implementation, but has a draft for it here: https://wiki.merproject.org/wiki/Middleware/PushNotifications
  
### UBports ###
  * UBports inherits the push infra implementation from Ubuntu Touch, but the push servers will get turned off soon.
  * The local client on the phone is written in Go 
  * It can route local as well as remote notifications
  * It is possible to either modify this client to follow a new approach or to enhance it with a companion process that delivers locally (But then the old functions should be deactivated)
  * The client requests a ticket from Ubuntu One (an OpenID provider) and passes this on to interested applications
  * Applications can use this ticket to send it on to App servers, which in turn will use it to deliver messages to the push server
  * The local client polls every 5-30min for new messages
  * The push server code is NOT open-sourced!