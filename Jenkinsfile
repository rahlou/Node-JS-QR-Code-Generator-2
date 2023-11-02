node('ubuntu-appserver-3120')
{
    def app 
    stage('Cloning Git')
    {
        checkout scm
    }

    stage('Build-and-Tag')
    {
        app = docker.build('quanch/qr_code_docker_repo')
    }

    stage('Post-to-Dockerhub')
    {
        docker.withRegistry('https://registry.hub.docker.com' , 'dockerhub_credentials')
        {
        app.push('latest')
        }
    }

    stage('Pull-image-server')
    {
        sh 'docker-compose down'
        sh 'docker-compose up -d'
    }
}