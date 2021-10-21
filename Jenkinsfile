pipeline {
    agent any 

    stages {
        stage('build'){
            steps {
                echo "build"
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