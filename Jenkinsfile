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
    def author = ""
    def changeSet = curBuild.rawBuild.changeSets               
    for (int i = 0; i < changeSet.size(); i++) 
    {
        def entries = changeSet[i].items
        println("First changeset loop")
        println()
        println(entries.inspect())

        def entry = entries[0]
        println()
        println(entry)
        author += "${entry.author}"
    }

    println("Serializing entire object")
    print author;
}
