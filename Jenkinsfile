
pipeline {
    agent any
    environment {
        EXAMPLE_KEY = credentials('example-credentials-id') // Secret value is 'sec%ret'
        // EXAMPLE_KEY2 = credentials('example2-credentials-id')
    }
    parameters {
        string(name: 'Greeting', defaultValue: 'Hello', description: 'How should I greet the world?')
        string(name: 'STATEMENT', defaultValue: 'hello; ls /', description: 'What should I say')
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
                // sh('echo ${STATEMENT}') is different from sh("echo ${STATEMENT}")
                // sh("echo ${STATEMENT}") is similar to sh('echo hello; ls /')
                sh('echo ${STATEMENT}')
                sh 'ls -la'
                sh 'echo $EXAMPLE_KEY'
                sh "echo $EXAMPLE_KEY"  // using Groovy String interpolation, which is insecure
                echo "${params.Greeting} World!"
            }
        }
    }
    post {
        failure {
            mail to: 'test@test.com',
            subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
            body: "Something is wrong with ${env.BUILD_URL}"
        }
        // success {
        //     mail to: 'test@test.com',
        //     subject: "succeeded Pipeline: ${currentBuild.fullDisplayName}",
        //     body: "${env.BUILD_URL} succeeded"
        // }
    }
}
