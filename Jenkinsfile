node {
    checkout scm
    sh 'docker network create bridge1';
    sh(script:'docker run --net bridge1 --name mysql-5 -d -e "MYSQL_ROOT_PASSWORD=my-secret-pw" -e "MYSQL_DATABASE=test" mysql:5.7', returnStdout: true)
    sh(script:'docker run --net bridge1 --name redis -d redis:5', returnStdout: true)

    docker.image('mysql:8-oracle').inside('--net bridge1 -e "DB_HOST=mysql-8" -e "REDIS_HOST=redis" -e "DB_DATABASE=test" -e "DB_USERNAME=root" -e "DB_PASSWORD=my-secret-pw"') {
        sh 'mysqladmin ping -hmysql-5 -uroot -pmy-secret-pw'
    }
    post { 
        always { 
            sh 'docker rm -f mysql redis; docker network rm bridge1';
        }
    }
}
