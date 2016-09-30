# docker-guide
Guide for docker


##Link with an external host:
  Add hostname mappings. Use the same values as the docker client --add-host parameter.

      extra_hosts:
       - "somehost:162.242.195.82"
       - "otherhost:50.31.209.229"

  An entry with the ip address and hostname will be created in /etc/hosts inside containers for this service, e.g:

      162.242.195.82  somehost
      50.31.209.229   otherhost
      
      
##Copy files:

    docker cp myFile mycontainer:myFile
    
##Export/Import

    echo     stop my-containerdb    
    docker stop db_my-container
    echo     stop my-container    
    docker stop back_my-container
    echo     stop engine_my-container    
    docker stop engine_my-container
    echo     stop my-container_front    
    docker stop www_my-container_front
    echo     stop my-container-t4html    
    docker stop www_my-container-t4htm

    echo     remove my-containerdb    
    docker rmi -f my-containerdb
    echo     remove my-container    
    docker rmi -f my-container
    echo     remove engine_my-container    
    docker rmi -f engine_my-container 
    echo     remove my-container_front    
    docker rmi -f my-container_front
    echo     remove my-container-t4html    
    docker rmi -f my-container-t4html


    echo     save my-containerdb    
    docker --host=10.1.43.241 save my-containerdb > my-containerdb.tar
    echo     save my-container    
    docker --host=10.1.43.241 save my-container > my-container.tar
    echo     save engine_my-container    
    docker --host=10.1.43.241 save my-container_engine > my-container_engine.tar
    echo     save my-container_front    
    docker --host=10.1.43.241 save  my-container_front > my-container_front.tar
    echo     save my-container-t4html    
    docker --host=10.1.43.241 save my-container-t4html > my-container-t4html.tar
    echo     save my-container-t4html    
    docker --host=10.1.43.241 cp www_my-container_front:usr/share/nginx/html html


    echo     load my-container    
    docker load < my-container.tar 
    echo     load my-container-t4html    
    docker load < my-container-t4html.tar
    echo     load my-containerdb    
    docker load < my-containerdb.tar
    echo     load my-container_front    
    docker load < my-container_front.tar
    echo     load my-container_engine    
    docker load < my-container_engine.tar 
    
    
##Run without compose

    docker stop www_my-container-t4html
    docker stop back_my-container
    docker stop engine_my-container
    docker stop www_my-container_front
    docker stop postgresqldb
    docker rm www_my-container-t4html
    docker rm back_my-container
    docker rm engine_my-container
    docker rm www_my-container_front
    docker rm postgresqldb
    docker network rm my-container-network
    docker volume rm www_my-container_front
    docker volume create --name www_my-container_front
    docker network create -d bridge my-container-network
    docker run --name postgresqldb --network my-container-network -e POSTGRES_PASSWORD=itesoft -d -p 9184:5432 -t my-containerdb:latest
    rem sleep hack
    ping -n 120 127.0.0.1 > nul

    docker run --name engine_my-container --network my-container-network -h engine.itesoft.local -d my-container_engine:latest
    docker run --name back_my-container --network my-container-network -v www_my-container_front:/usr/share/nginx/html/  -d -p 9199:8000 -p 9186:8080  -t my-container:latest
    docker run --name www_my-container_front --network my-container-network -d -p 8080:80  -v www_my-container_front:/usr/share/nginx/html/ -t my-container_front:latest
    docker cp html/0-Base www_my-container_front:/usr/share/nginx/html/
    docker run --name www_my-container-t4html --network my-container-network -d -p 9189:80 -v /generator -t my-container-t4html:latest
