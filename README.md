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

        sudo systemctl dameon-reload
        sudo systemctl docker restart
