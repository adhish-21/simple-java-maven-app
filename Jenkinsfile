pipeline {
    agent {
        docker {
            image 'maven:3.9.2'
            args '-v /var/jenkins_home/m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -Dmaven.repo.local=/root/m2/repository -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn -Dmaven.repo.local=/root/m2/repository test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
