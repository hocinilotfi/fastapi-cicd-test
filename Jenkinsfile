pipeline{

    agent {
        docker {
            image "postman/newman"
            args "--entrypoint=''"
        }
        
    }
    triggers { upstream(upstreamProjects: 'fastapi-cicd', threshold: hudson.model.Result.SUCCESS) }

    stages{
        stage('verifier la version de newman'){
            steps{
                sh 'newman --version'
            }
        }
        stage('Test API'){
            steps{
                sh 'newman run ma-collection.json -r cli,junit --reporter-junit-export="newman-report.xml"'
            }
        }
    }
    post{
        always {
            junit 'newman-report.xml'
            archiveArtifacts artifacts: 'newman-report.xml'
        }
    }
}