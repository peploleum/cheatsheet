# cheatsheet
reminder for various CLI

## Docker for Windows

    docker system prune -a
    docker rm $(docker ps -a -f status=exited -q)
