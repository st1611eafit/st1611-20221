# st1611-20221 - Edwin Montoya - emontoya@eafit.edu.co

## instalación de docker en amazon AMI2

### Instalar docker en linux-ami2

    sudo amazon-linux-extras install docker -y
    sudo yum install git -y

    sudo systemctl enable docker
    sudo systemctl start docker
    sudo usermod -a -G docker ec2-user

    pip3 install docker-compose

## ejecutar wordpress en un solo servidor con docker:

    referencia: https://hub.docker.com/_/wordpress

    mkdir wordpress-monoserver
    cd wordpress-monoserver
    cp ../docker-compose-wordpress-monoserver.yml docker-compose.yml

    para subirlo:

    docker-compose up -d

    desde un browser entrar a: http:<ip-publica>

    para bajarlo:

    docker-compose down

# ejecutar wordpress en dos servidores con docker:

## wordpress-db servidor2

    mkdir wordpress-db
    cd wordpress-db
    cp ../docker-compose-wordpress-server2db.yml docker-compose.yml

    para subirlo:

    docker-compose up -d

    para bajarlo:

    docker-compose down

## wordpress-web servidor1

    mkdir wordpress-web
    cd wordpress-web
    cp ../docker-compose-wordpress-server1web.yml docker-compose.yml

    ACTUALICE LA IP DEL <ip-server-db> en 'docker-compose.yml' con la IP del servidor2 anterior

    para subirlo:

    docker-compose up -d

    desde un browser entrar a: http:<ip-publica>

    para bajarlo:

    docker-compose down