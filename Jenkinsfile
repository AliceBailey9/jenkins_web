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
        stage("package html"){
            steps{
                sh """
                mkdir -p build
                cp index.html build/index.html
                tar -zcvf build.tgz build
                """
            }
        }
        stage("Artifacts HTML"){
            steps{
                archiveArtifacts artifacts: "build.tgz", followSymLinks: false
            }
        }

        stage('deploy/ssh copy'){
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'http', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'mv index.html www/var/index', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'index.html')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
post {
    always {
       archiveArtifacts artifacts: "build.tgz", followSymLinks: false
    }
}
}