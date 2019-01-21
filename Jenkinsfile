
class GitChangeSetObj implements Serializable {
    String build_id
    String commit_id
    String author
    String email
    String comment

    GitChangeSetObj(build_id, commit_id, author, email, comment){
        this.build_id = build_id
        this.commit_id = commit_id
        this.author = author
        this.email = email
        this.comment = comment
    }

}

@NonCPS
def getCulprits(build){
    culprits = []

    if(build.properties.changeSets[0] != null){
       for (changeSet in build.properties.changeSets){
          for (change in changeSet){
              GitChangeSetObj git_change_set = new GitChangeSetObj(
                  build.displayName.toString(),
                  change.id,
                  change.author,
                  change.authorEmail,
                  change.comment
              )
              culprits.add(git_change_set)
              //println "author " + change.author
          }
       }
    }

    return culprits
}

@NonCPS
def last_change_sets() {
    def list = []
    for (changeSets in currentBuild.changeSets) {
        for (items in changeSets.items) {
            for (files in items.affectedFiles) {
                list.add( files.path.split('/')[0] )
            }
        }

    }
    return list
}

def get_emails(culprit_list) {
  def list = []
  for (culprit in culprit_list){ 
    list.add(culprit.author + ":" + culprit.email )
  } 
  return list
}

@NonCPS
def get_userId() {
    return currentBuild.getBuildCauses()
}

@NonCPS
def getBuildUser() {
    return currentBuild.rawBuild.getBuildCauses(Cause.UserIdCause).getUserId()
}

def get_cause() {
    def buildCauses = currentBuild.rawBuild.getCauses()
    for ( buildCause in buildCauses ) {
        if (buildCause != null) {
            def causeDescription = buildCause.getShortDescription()
            echo "shortDescription: ${causeDescription}"
            if (causeDescription.contains("Started by timer")) {
                startedByWhat = 'timer'
            }
            if (causeDescription.contains("Started by user")) {
                startedByWhat = 'user'
            }
        }
    }
}

def cause() {
	def causes = currentBuild.getBuildCauses()
	for (cause in causes) {
		println cause.toString()
		println cause["shortDescription"]
	}
}
//node {
//	echo "Hello world"
//	cause()
//}

pipeline {

    agent any
    environment {
        def userId = "${env.UID}";
    }
    stages {
	    stage ("Check") {
			steps {
				// want to exit success
				script {currentBuild.result = 'SUCCESS'} 
				 
				// Abort the build, skipping subsequent stages
				//error("Invalid target environment")
				cause()
			}
		}
        stage('Print UID') { 
            steps {
                script {
                   echo get_cause()
                }
            }
        }
    }
}
//node {
//   checkout scm
   //def aci = last_change_sets()
   //println aci

//   println "Culprits list:"
//   def cpl = getCulprits(currentBuild)
//   println get_emails(cpl)
   
//   echo 'user id:'
//   echo currentBuild.getBuildCauses(hudson.model.Cause$UserIdCause)
   
//   sh 'echo Done'
//   sh 'ls -la'
   
//}

