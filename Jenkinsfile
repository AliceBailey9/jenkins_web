def printFromFunction() {
    println('I am printing in a function')
}

pipeline {
    agent any 

    options {
        timestamps()
    }

    stages {
        stage('build'){
            steps {
                echo "building"
                printFromFunction()
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