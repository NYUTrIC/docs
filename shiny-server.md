Accessing production server via ssh tunneling:
KID: kerberos ID
server_name will be something like #nyumc.org@{}@psmp.nyumc.org

ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeychecking=no KID@KID{server_name}


Copying files from local machine to production server (uploading apps):
destination: full path to desired locale in production server
src_: full path to local file (or, here foler with code as '-r' recursive flag is set)

scp -o UserKnownHostsFile=/dev/null -o StrictHostKeychecking=no -r -v -O ${src_} KID@KID{server_name}:${destination} 

shiny apps locale on server:
/srv/shiny-server

from README.txt @ shiny locale:
##

General log file: /var/log/shiny-server.log
App-specific log files: /var/log/shiny-server/*.log

Make sure you are part of the `shiny` group.

Make sure the files in each directory/app are accessible by all:
`chmod -Rc a+rX .`

Install R packages globally as root (run `sudo R`).

## 

Additional notes:
1. In order to edit max memory for applications:
  sudo vim /etc/nginx/nginx.conf
  add client_max_body_size 1000M; for 1000 megs (1 GB) to http{} block
  sudo nginx -s reload