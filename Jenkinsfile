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
                    sh "bash testFile.sh"
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
                sshPublisher(publishers: [sshPublisherDesc(configName: 'http', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'my index.html www/var/index', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'index.html')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}