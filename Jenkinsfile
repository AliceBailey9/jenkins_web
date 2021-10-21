def printFromFunction() {
    println('I am printing in a function')
}

def replaceString() {
    def text = readFile file: "index.html"
    text = text.replaceAll("%BUILD_NUMBER%", "${BUILD_NUMBER}")
    writeFile file: "index.html" , text: text
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
                replaceString()
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