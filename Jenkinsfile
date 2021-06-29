
pipeline {
    agent any
    parameters {
        string(name: 'STATEMENT', defaultValue: 'hello', description: 'What should I say')
    }
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
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
            steps {
                echo "${currentBuild.result}"
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            }
        }
    }
}
