node {
    checkout scm
    sh 'docker network create bridge1';
    sh(script:'docker run --net bridge1 --name mysql -d -e "MYSQL_ROOT_PASSWORD=my-secret-pw" -e "MYSQL_DATABASE=test" mysql:5.7', returnStdout: true)
    sh(script:'docker run --net bridge1 --name redis -d redis:5', returnStdout: true)
    def testImage = docker.build("test-image:${env.BUILD_ID}", "-f Dockerfile ./")
    testImage.inside('--net bridge1 -e "DB_HOST=mysql" -e "REDIS_HOST=redis" -e "DB_DATABASE=test" -e "DB_USERNAME=root" -e "DB_PASSWORD=my-secret-pw"') {
        stage('Prepare') {
            echo 'preparing'
            sh 'env'
            sh 'apt-get update && apt-get install -y librsvg2-bin'
        }
        stage('Test') {
            echo 'testing...'
            sh 'ls'
        }
    }
}
