
@NonCPS
def last_change_sets() {
	def changeLogSets = currentBuild.changeSets
	println "must be here..."
	for (int i = 0; i < changeLogSets.size(); i++) {
	    println "here..."
		def entries = changeLogSets[i].items
		for (int j = 0; j < entries.length; j++) {
			def entry = entries[j]
			def files = new ArrayList(entry.affectedFiles)
			for (int k = 0; k < files.size(); k++) {
				def file = files[k]
				def arr = file.path.split('/')
				println arr[0]
			}
		}
	}
}

node {
   checkout(scm)
   last_change_sets()
   sh 'echo Done'
}
