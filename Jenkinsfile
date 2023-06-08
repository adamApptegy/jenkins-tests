pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                git (url: 'https://github.com/adamApptegy/jenkins-tests.git', branch: 'main')
                script {
                    println(currentBuild.changeSets) // should print an empty set
                }
            }
        }
    }
}
