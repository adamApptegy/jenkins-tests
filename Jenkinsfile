pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    def output = sh(script: 'git diff origin/main --name-only', returnStdout: true)
                    echo output
                    processDiff(output)
                }
            }
        }
    }
}

@NonCPS
def processDiff(diffOutput) {
    for (line in diffOutput.split("\n")) {
        println(line)
    }
}