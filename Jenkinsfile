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
@NonCPS
def get_cause() {
	//return currentBuild.rawBuild.getCauses()
	//return currentBuild.causes[0]
	//return ${BUILD_CAUSE}
    currentBuild.rawBuild.getCauses().toString()
}

node {
   checkout(scm)
   println last_change_sets()
   echo get_cause()
   echo currentBuild.buildCauses
   sh 'echo Done'
}

