def PROJECTS = [
    FIRST_PROJECT: [
        prod: [
            someKey: 'someValue'
        ]
    ],
    SECOND_PROJECT: [
        notprod: [
            someKey: 'someValue'
        ]
    ]
]

pipeline {
    agent any
    stages {
        stage("Run tests on branch change") {
            when {
                expression {
                    return env.BRANCH_NAME != 'master';
                }
            }
            steps {
                script {
                    def output = sh(script: 'git diff origin/main --name-only', returnStdout: true)
                    echo output
                    processDiff(output)
                }
            }
        }
        stage('Loop') {
            steps {
                script {
                    PROJECTS.each() {
                        echo it
                    }
                }
            }
        }
    }
}
// change
@NonCPS
def processDiff(diffOutput) {
    for (line in diffOutput.split("\n")) {
        println(line)
    }
}