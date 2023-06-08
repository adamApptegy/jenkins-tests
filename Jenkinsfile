pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                git (url: 'https://github.com/adamApptegy/jenkins-tests.git', branch: 'main')
                script {
                    def changeSets = allChangeSetsFromLastSuccessfulBuild()
                    echo "ChangeSet Size : ${changeSets.size()}"
                    echo "Files Changed : ${getFilesChanged(changeSets)}"
                }
            }
        }
    }
}

def allChangeSetsFromLastSuccessfulBuild() {
    def job = Jenkins.instance.getItem("$JOB_NAME")
    def lastSuccessBuild = job.lastSuccessfulBuild.number as int
    def currentBuildId = "$BUILD_ID" as int
    
    def changeSets = []

    for(int i = lastSuccessBuild + 1; i < currentBuildId; i++) {
        echo "Getting Change Set for the Build ID : ${i}"
        def chageSet = job.getBuildByNumber(i).getChangeSets()
        changeSets.addAll(chageSet)
    }
     changeSets.addAll(currentBuild.changeSets) // Add the current Changeset
     return changeSets
}

def getFilesChanged(chgSets) {
    def filesList = []
    def changeLogSets = chgSets
        for (int i = 0; i < changeLogSets.size(); i++) {
            def entries = changeLogSets[i].items
            for (int j = 0; j < entries.length; j++) {
                def entry = entries[j]
                def files = new ArrayList(entry.affectedFiles)
                    for (int k = 0; k < files.size(); k++) {
                    def file = files[k]
                    filesList.add(file.path)
            }
        }
    }
    return filesList
}
