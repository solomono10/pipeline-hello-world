pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                sh 'chmod +x hello-world.sh'
                sh './hello-world.sh'
            }
        }
        stage('Test') { 
            steps {
                echo 'Hello man'
            }
        }
        stage('Deploy') { 
            steps {
                echo 'Hello woman' 
            }
        }
    }
}