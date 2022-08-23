# SAP NW ABAP 7.52 SP04 Trial in Docker

## Instructions

1. ### Install [Docker](https://www.docker.com/community-edition)

1. ### Create .wslconfig file in `C:\Users\<UserName>)`:
    ```sh
    [wsl2]
    memory=6GB
    processors=4
    swap=2GB
    kernelCommandLine=sysctl.vm.max_map_count=1000000
     ```
        
1. Clone this repo

    ```sh
    git clone https://github.com/nzamani/sap-nw-abap-trial-docker.git
    cd sap-nw-abap-trial-docker
    ```
    
1. Download [SAP NW ABAP 7.52 SP01 Trial from SAP](https://developers.sap.com/germany/trials-downloads.html) (search for **7.52**), then:
    create a folder `sapdownloads` inside the clone
    extract TD752SP04.part01.rar to /sapdownloads
    extract Licence.rar
    copy `SYBASE_ASE_TestDrive` to `sapdownloads\server\TAR\x86_64\`
  
1. build container
    ```sh
    docker build -t nwabap:7.52 .
    wsl -d docker-desktop  
    sysctl -w vm.max_map_count=1000000  
    exit  
    ```

    ```sh
    docker run --privileged -p 8000:8000 -p 44300:44300 -p 3300:3300 -p 3200:3200 -h vhcalnplci --name nwabap752 -it nwabap:7.52 /bin/bash
    ```
    
    check via `sysctl vm.max_map_count` 

1. Start installation:
    ```sh
    /usr/sbin/uuidd
    chmod u+s /bin/ping
    ./custom_install.sh
    ```
    
   `Your installation has been successful if you see the followong message: **Installation of NPL successful**`

1. Starting the container + SAP NW ABAP Trial (use this from now on instead of `docker run ...` from above)

    ```sh
    docker start -i nwabap752
    /usr/sbin/uuidd
    su npladm
    startsap ALL
    ```

1. Stopping SAP NW ABAP Trial and container (`ALL` can be omitted)

    ```sh
    su npladm
    stopsap ALL
    exit
    exit
    ```
