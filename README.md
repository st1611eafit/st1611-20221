# ST1611-20221 - Edwin Montoya - emontoya@eafit.edu.co

## instalación de docker en amazon AMI2

### Instalar docker en linux-ami2

    sudo amazon-linux-extras install docker -y
    sudo yum install git -y

    sudo systemctl enable docker
    sudo systemctl start docker
    sudo usermod -a -G docker ec2-user

    pip3 install docker-compose
    exit

# clonar el repositorio github del curso:

    git clone https://github.com/st1611eafit/st1611-20221.git

## correr docker-compose como un servicio del sistema operativo

    Configuración para cada que baje y suba la máquina, ejecute docker-compose up -d

### 1.	Instale a nivel de root, el docker-compose

    sudo su
    pip3 install docker-compose 
    exit

### 2.	Modifique el archivo ‘docker-compose-app.service’ a su conveniencia

    mkdir app

    copie los archivos docker-compose.yml y demás archivos que requiera en la carpeta 'app'
    
    cp docker-compose.yml $HOME/app/
    cp $HOME/st1611-20221/docker-compose-app.service $HOME/app/
    nano $HOME/app/docker-compose-app.service
    
    sudo cp $HOME/app/docker-compose-app.service /etc/systemd/system/
    sudo systemctl enable docker-compose-app
    sudo systemctl start docker-compose-app

## ejecutar wordpress en un solo servidor con docker:

    referencia: https://hub.docker.com/_/wordpress

    mkdir $HOME/wordpress-monoserver
    
    cp $HOME/st1611-20221/docker-compose-wordpress-monoserver.yml $HOME/wordpress-monoserver/docker-compose.yml

    para subirlo:

    cd $HOME/wordpress-monoserver
    docker-compose up -d

    desde un browser entrar a: http:<ip-publica>

    para bajarlo:
    cd $HOME/wordpress-monoserver
    docker-compose down

# ejecutar wordpress en dos servidores con docker:

## wordpress-db servidor2

    mkdir $HOME/wordpress-db
    
    cp $HOME/st1611-20221/docker-compose-wordpress-server2db.yml $HOME/wordpress-db/docker-compose.yml

    para subirlo:
    cd $HOME/wordpress-db
    docker-compose up -d

    para bajarlo:
    cd $HOME/wordpress-db
    docker-compose down

## wordpress-web servidor1

    mkdir $HOME/wordpress-web
    cp $HOME/st1611-20221/docker-compose-wordpress-server1web.yml $HOME/wordpress-web/docker-compose.yml

    ACTUALICE LA IP DEL <ip-server-db> en 'docker-compose.yml' con la IP del servidor2 anterior

    para subirlo:
    cd $HOME/wordpress-web
    docker-compose up -d

    desde un browser entrar a: http:<ip-publica>

    para bajarlo:

    cd $HOME/wordpress-web
    docker-compose down

## ejecutar nginx-wordpressweb-wordpressdb monolitico - monoservidor:

    mkdir $HOME/nginx-all

    cp $HOME/st1611-20221/docker-compose-nginx-wordpress-monoserver.yml $HOME/nginx-all/docker-compose.yml

    para subirlo:
    cd $HOME/nginx-all
    docker-compose up -d

    desde un browser entrar a: http:<ip-publica>

    para bajarlo:

    cd $HOME/nginx-all
    docker-compose down

## ejecutar nginx como proxy inverso de un servidor wordpress-web posiblemente en una subred privada:

    mkdir $HOME/nginx

    cp $HOME/st1611-20221/docker-compose-nginx.yml $HOME/nginx/docker-compose.yml

    configure el nginx.conf con la dirección real del servidor wordpress-web

    para subirlo:
    cd $HOME/nginx
    docker-compose up -d

    desde un browser entrar a: http:<ip-publica>

    para bajarlo:
    cd $HOME/nginx
    docker-compose down
