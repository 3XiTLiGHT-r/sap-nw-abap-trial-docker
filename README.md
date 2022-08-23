# sap-nw-abap-trial-docker
AS ABAP 752 SP04 Trial in Docker

docker build -t nwabap:7.52 .  

wsl -d docker-desktop  
sysctl -w vm.max_map_count = 1000000  
exit  

docker run --privileged -p 8000:8000 -p 44300:44300 -p 3300:3300 -p 3200:3200 -h vhcalnplci --name nwabap752 -it nwabap:7.52 /bin/bash  

/usr/sbin/uuidd  
chmod u+s /bin/ping  
./install.sh  
