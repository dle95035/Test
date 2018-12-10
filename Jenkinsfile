
def last_change_sets() {
        def changeLogSets = currentBuild.changeSets
        def list = []
        for (int i = 0; i < changeLogSets.size(); i++) {
                def entries = changeLogSets[i].items
                for (int j = 0; j < entries.length; j++) {
                        def entry = entries[j]
                        def files = new ArrayList(entry.affectedFiles)
                        for (int k = 0; k < files.size(); k++) {
                                list.add( files[k].path.split('/')[0] )
                        }
                }
        }
        return list
}

node {
   checkout(scm)
   println last_change_sets()
   sh 'echo Done'
}

