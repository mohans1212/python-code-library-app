pipeline{
    agent any
    environment{
        NAME = "${BUILD_TAG}:${BUILD_ID}"
    }
    stages{
        stage("Code Checkouts"){
            steps{
                git branch: 'master', url: 'https://github.com/mohans1212/python-code-library-app'            }
        }  
        stage("Build Images"){
            steps{
                sh 'docker build -t dbimage database/'
                sh 'docker build -t authimage auth/'
                sh 'docker build -t bookimage book/'
                sh 'docker build -t borrowimage borrow/'
                sh 'docker build -t appimage .'
            }
        }
        stage("Deploy Containers"){
            steps{

                sh 'docker stop $(docker ps -a -q) || true'
                sh 'docker rm $(docker ps -a -q) || true'
                sh 'docker run -d --name dbcontainer --network mynet dbimage'
                sh 'docker run -d --name authcontainer --network mynet authimage'
                sh 'docker run -d --name bookcontainer --network mynet bookimage'
                sh 'docker run -d --name borrowcontainer --network mynet borrowimage'
                sh 'docker run -d --name frontend -p 5000:5000 --network mynet appimage'
           
            }
        }
    }
}