@Library('jenkins_shared') _

pipeline {
    agent any 

    options {
        timestamps()
    }

    stages {
        stage('build'){
            steps {
                echo "building"
                helloVariable("Alice")
                script {
                    utils.replaceString()
                }
            }
        }

        stage('test'){
            parallel {

                stage("test on windows"){
                    steps {
                        echo "test on windows"
                    }

                } 
                stage("test on linux"){
                    steps {
                        echo"test on linux"
                    }
                }
            }
        }

        stage('deploy'){
            steps {
                echo "deploy"
            }
        }
    }
}