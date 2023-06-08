pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                git (url: 'https://github.com/adamApptegy/jenkins-tests.git', branch: 'main')
                script {
                    getChangeSet(currentBuild)
                }
            }
        }
    }
}

def getChangeSet(curBuild) {
    println("getting changesetsome")
    def changeSet = curBuild.changeSets

    println(changeSet)

    changeSet.each{change ->
        println(change)
    }
   
}
