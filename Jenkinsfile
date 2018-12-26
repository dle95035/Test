
@NonCPS
def getCulprits(build){
    def culprits = []
    for (changeSets in build.properties.changeSets) {
        for (items in changeSets.items) {
			culprits.add(items.authorEmail)
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
   println cpl
   echo get_cause()
   sh 'echo Done'
   sh 'ls -la'
   
   mail (to: 'dle95035@yahoo.com',
         subject: "This is from Jenkins",
         body: "Testing!!!");
}

