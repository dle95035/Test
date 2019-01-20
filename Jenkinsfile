
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
    list.add(culprit.author + ":" + culprit.email + ":" + culprit.id)
  } 
  return list
}

@NonCPS
def get_cause() {
    return currentBuild.getBuildCauses(Cause.UserIdCause)
}

@NonCPS
def getBuildUser() {
    return currentBuild.getBuildCauses(Cause.UserIdCause).getUserId()
}

node {
   checkout scm
   //def aci = last_change_sets()
   //println aci

   println "Culprits list:"
   def cpl = getCulprits(currentBuild)
   println get_emails(cpl)
   
   echo 'user id:'
   echo get_cause()
   
   sh 'echo Done'
   sh 'ls -la'
   
}

