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
    println("getting changeset")
    def author = ""
    def changeSet = curBuild.rawBuild.changeSets               
    for (int i = 0; i < changeSet.size(); i++) 
    {
        def entries = changeSet[i].items
        println("First changeset loop")
        println(entries)
        def entry = entries[0]
        println(entry)
        author += "${entry.author}"
    }

    println("Serializing entire object")
    println(groovy.json.JsonOutput.toJson(curBUild.rawBuild.changeSets))
    print author;
}
