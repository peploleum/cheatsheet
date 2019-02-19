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


        sudo -i
        partprobe
        resize2fs /dev/vda1
        mkswap /dev/vda2


Copy uuid and replace in /etc/fstab
        
        
        swapon -a
