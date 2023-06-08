pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                git (url: 'https://github.com/adamApptegy/jenkins-tests.git', branch: 'main')
                script {
                    showChangeLogs()
                }
                script {
                    def output = sh(returnStatus: true, script: 'git diff origin/main --name-only', returnStdout: true)
                    echo output
                }
            }
        }
    }
}


@NonCPS
def showChangeLogs() {
  def changeLogSets = currentBuild.rawBuild.changeSets
  for (int i = 0; i < changeLogSets.size(); i++) {
     def entries = changeLogSets[i].items
     for (int j = 0; j < entries.length; j++) {
          def entry = entries[j]
          echo "${entry.commitId} by ${entry.author} on ${new Date(entry.timestamp)}: ${entry.msg}"
          def files = new ArrayList(entry.affectedFiles)
          for (int k = 0; k < files.size(); k++) {
              def file = files[k]
              echo "  ${file.editType.name} ${file.path}"
          }
      }
  }
}