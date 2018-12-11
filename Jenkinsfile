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

def get_cause() {
	//return currentBuild.rawBuild.getCauses()
	return currentBuild.causes[0]
}

node {
   checkout(scm)
   println last_change_sets()
   println get_cause()
   sh 'echo Done'
}

