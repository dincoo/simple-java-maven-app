pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /Users/jaden/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
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
                input 'Finished using the web site? (Click "Proceed" to continue)'
            }
        }
    }
}
