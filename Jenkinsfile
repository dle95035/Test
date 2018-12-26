
@NonCPS
getCulprits(build){
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
          }
       }
    }

    return culprits
}

@NonCPS
def last_change_sets() {
    def list = []
    for (changeSets in currentBuild.properties.changeSets) {
        for (items in changeSets.items) {
            for (files in items.affectedFiles) {
                list.add( files.path.split('/')[0] )
            }
        }

    }
    return list
}
@NonCPS
def get_cause() {
    currentBuild.getBuildCauses().toString()
}

node {
   checkout scm
   def aci = last_change_sets()
   println aci
   def cpl = getCulprits(currentBuild)
   echo get_cause()
   sh 'echo Done'
   sh 'ls -la'
}

