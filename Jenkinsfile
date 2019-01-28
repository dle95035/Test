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
    
    if ( 1 == currentBuild.changeSets.size()	) { 
	    println "changeset"
		if ( 1 == currentBuild.changeSets[0].items.size() ) { 
			println "items"
			if ( 1 == currentBuild.changeSets[0].items[0].affectedPaths.size() ) { 
				println "affectedFiles"
				fullFileName = currentBuild.changeSets[0].items[0].affectedPaths[0]
				println fullFileName
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
                 getChangeFile()
             }
         }
     }
}
