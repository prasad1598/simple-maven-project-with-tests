currentBuild.displayName = "Final_Demo # "+currentBuild.number

   def getDockerTag(){
        def tag = sh script: 'git rev-parse HEAD', returnStdout: true
        return tag
        }
pipeline {
    agent any
    environment {
        BUILD_COMPLETE = false
    }
    stages {
        stage('Build') {
            failFast true
            parallel {
                stage('Building') {
                    steps {
                        
                        sh "mvn deploy |  tee output.log"

                        sh '! grep "WARNING" output.log'

                        script {
                            BUILD_COMPLETE = true
                        }
                    }
                }
                stage('Monitoring the logs') {
                    steps {
                        script {
                            while (BUILD_COMPLETE != true) {
                                sh '! grep "WARNING" output.log'
                            }
                        }
                    }
                }
            }
        }
    }
}
