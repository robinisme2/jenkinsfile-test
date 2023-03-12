node {
    checkout scm
    sh 'docker network create bridge1';
    sh(script:'docker run --net bridge1 --name mysql -d -e "MYSQL_ROOT_PASSWORD=my-secret-pw" -e "MYSQL_DATABASE=test" mysql:5.7', returnStdout: true)
    sh(script:'docker run --net bridge1 --name redis -d redis:5', returnStdout: true)

    docker.image('mysql:8-oracle').inside('--net bridge1 -e "DB_HOST=mysql" -e "REDIS_HOST=redis" -e "DB_DATABASE=test" -e "DB_USERNAME=root" -e "DB_PASSWORD=my-secret-pw"') {
        sh 'mysqladmin ping -h$DB_HOST'
    }
    sh 'docker rm -f mysql redis';
}
