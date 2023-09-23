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

def parallelStagesMap = PROJECTS.collectEntries {
    ["${it.key}" : generateStage(it)]
}

def generateStage(job) {
    return {
        stage("stage: ${job.key}") {
                echo "This is ${job.key}."
                sh script: "sleep 15"
        }
    }
}


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
        stage('Loop') {
            steps {
                script {
                    parallel parallelStagesMap
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