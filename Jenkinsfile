pipeline {

    agent any 

    options {
        timestamps()
    }

    stages {
        stage("my first stage"){
            steps {
                echo "this is my step in my first stage, yay!"
            }
        }
        stage('print environment variables'){
            steps {
                sh "printenv"
            }
        }
    }
}