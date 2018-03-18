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
                        echo "M2_HOME = ${M2_HOME"
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
                    echo "This is Deploy job"
                }
        }
}
}