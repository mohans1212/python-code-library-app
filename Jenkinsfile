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
    }
}