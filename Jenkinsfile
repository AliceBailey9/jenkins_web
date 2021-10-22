@Library('jenkins_shared') _

pipeline {
    agent any 

    options {
        timestamps()
    }

    environment {
        MYENVVAR ="testenvvar"
    }

    parameters{
        string(name: 'Name', defaultValue: 'Bailey', description:'My surname')
    }

    stages {
        stage('build'){
            steps {
                echo "building"
                echo "${MYENVVAR}"
                echo "${params.Name}"
                helloVariable("Alice")
                script {
                    utils.replaceString()
                }
            }
        }
        stage('docker build'){
            agent {
                docker {
                    image "node:latest"
                    arg "-v ${WORKSPACE}/docker:/home/node"
                }
            }
            steps {
                sh """
                node --version > /home/node/docker_node_version
                npm --version > /home/node/docker_npm_version
                """
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
                archiveArtifacts artifacts: "build.tgz", followSymlinks: false
            }
        }

        stage('deploy/ssh copy'){
            steps {
sshPublisher(publishers: [sshPublisherDesc(configName: 'http', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'tar  -zxvf build.tgz && mv build/index.html /var/www/html/index.html', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'build.tgz')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])            }
        }
    }
post {
    always {
       archiveArtifacts artifacts: "build.tgz", followSymlinks: false
    }
}
}