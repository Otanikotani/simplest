pipeline {
    agent {label 'slave'}
    stages {
        stage("Build") {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }

        stage("Unit Tests") {
            steps {
                sh './mvnw test'
            }
        }

        stage("Dockerized") {
            agent { dockerfile true }
            
        }
    }

    post {
        always {
            echo 'Pipeline has ended'
            archiveArtifacts '**/target/*.jar'
            archiveArtifacts '**/target/*.jar'
            junit('**/surefire-reports/**/*.xml')
        }
        success {
            echo 'The pipeline was successful'
        }
        failure {
            echo 'The pipeline failed'
        }
        unstable {
            echo 'The pipeline is unstable'
        }
        changed {
            echo 'The pipeline state has changed'
        }
    }
}