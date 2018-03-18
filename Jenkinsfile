pipeline{
    agent any
        tools{
            jdk "JenkinsJAva"
            maven "MavenTraining"
        }
        stages{
            stage("Init"){
                steps{
                    sh'''
                        echo "PATH = ${PATH}"
                        echo "M2_HOME = ${M2_HOME}"
                    '''
                }
            }
            stage("Build"){
                steps{
                    sh 'mvn clean package checkstyle:checkstyle'
                }
                post{
                    success{
                        echo "Archive the artifacts"
                        archiveArtifacts '**/*.war'
                        echo "Check Junit Result"
                        junit '**/target/surefire-reports/*.xml'
                        echo "Checkstyle result"
                        checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: ''
                    }
                }
            }
            stage("Deploy"){
                steps{
                    build 'deploy_to_dev'
                }
            }
            stage("Delivery"){
                steps{
                    timeout(2) {
                        input 'Want to proceed for Production deployment?'
                    }
                    build 'deploy_to_prod'
                }
            }  
        }
}