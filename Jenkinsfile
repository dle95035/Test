def isOnlyVersionBump() {
    def fullFileName = ""
    for (changeSet in currentBuild.changeSets) {
        for (item in changeSet.items) {
            for (file in item.affectedFiles) {
                if ( 1 < item.affectedFiles.size() ) {
                    return false
                }
                fullFileName = file.path
                if ( "version.sbt" == fullFileName.substring(fullFileName.lastIndexOf("/")+1) ) {
                    return true
                }
            }
        }
    }
    return false
}

def getChangeFile() {
    def fullFileName
    if ( 1 == currentBuild.changeSets.size()	) { 
		if ( 1 == currentBuild.changeSets[0].items.size() ) { 
			if ( 1 == currentBuild.changeSets[0].items[0].affectedFiles.size() ) { 
				fullFileName = currentBuild.changeSets[0].items[0].affectedFiles.first().path
				if ( "version.sbt" == fullFileName.substring(fullFileName.lastIndexOf("/")+1) ) {
					return true
				}
			}
		}
	}
	return false
}

pipeline {
    agent any

     stages {
         stage('Clone repository and build tests') {
             steps {
                 sh 'ls -la'
                 println getChangeFile()
             }
         }
     }
}
