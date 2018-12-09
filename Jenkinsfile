
@NonCPS
def last_change_sets() {
    def list = []
	def changeLogSets = currentBuild.changeSets
	for (int i = 0; i < changeLogSets.size(); i++) {
		def entries = changeLogSets[i].items
		for (int j = 0; j < entries.length; j++) {
			def entry = entries[j]
			def files = new ArrayList(entry.affectedFiles)
			for (int k = 0; k < files.size(); k++) {
				def file = files[k]
				def arr = file.path.split('/')
				//println arr[0]
				list.add(arr[0])
			}
		}
	}
	println list
}

node {
   checkout(scm)
   //def projects = last_change_sets()
   //println projects
   sh 'echo Done'
}
