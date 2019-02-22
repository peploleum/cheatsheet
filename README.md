# cheatsheet
reminder for various CLI

## Docker for Windows

    docker system prune -a
    docker rm $(docker ps -a -f status=exited -q)
    
## Docker for Linux

* enable IPV6: edit /etc/docker/daemon.json

        {
        "debug": true,
        "ipv6": true,
        "fixed-cidr-v6": "2001:db8:1::/64",
        "hosts": ["unix:///var/run/docker.sock", "tcp://127.0.0.1:2375"]
        }
        
* restart docker

        sudo systemctl dameon-reload
        sudo systemctl docker restart

## Misc

        df -hT
        du -hd1 /

ubuntu 16.04 resize boot volume (e.g. /dev/vda1)

        sudo fdisk /dev/vda
        
* Make note of the start cylinder of /dev/vda1 using "p"
* "d" delete first the swap partition (2) and then the /dev/vda1 partition. This is very scary but is actually harmless as the data is not written to the disk until you write the changes to the disk.
* "n" to create a new primary partition. Make sure its start cylinder is exactly the same as the old /dev/vda1 used to have. 
* "a" to toggle the bootable flag on the new /dev/sda1
* "w" to commit changes

        sudo -i
        partprobe
        resize2fs /dev/vda1
        mkswap /dev/vda2


Copy uuid and replace in /etc/fstab
        
        
        swapon -a


pretty append

         echo 'dns-search openstacklocal corp.capgemini.com' | sudo tee -a /etc/network/interfaces
         echo 'dns-nameservers 66.28.0.45 66.28.0.61 127.0.1.1' | sudo tee -a /etc/network/interfaces
         
## vim

> select block: v  
> copy selection: y  
> paste: P  
> jump to eol and edit: A  
> search: /  
> replace crlf eols: %s/^M//g  
To enter ^M, type CTRL-V, then CTRL-M

## Docker internet access ubuntu 16.04

        vi /etc/default/docker
        
add following commands
        
        # Use DOCKER_OPTS to modify the daemon startup options.
        DOCKER_OPTS="--dns 8.8.8.8 --dns 8.8.4.4"

## Kubernetes on Ubuntu 18.04
>disable swap after reboot

        sudo vi /etc/fstab
        comment UUID line
        sudo shutdown -r now
