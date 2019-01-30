def isOnlyVersionBump() {

    // full path file name.
    def fullFileName
	
	if (null != currentBuild.changeSets) {
		def changeSets = currentBuild.changeSets
	} else {
		return false
	}
    if (changeSets[0].items) {
		def items = changeSets[0].items
	} else {
		return false
	}
	if (items[0].affectedFiles) {
		def affectedFiles = items[0].affectedFiles
	} else {
		return false
	}

    // single changeSet, 2 items , single affectedFile
    if ( 1 == changeSets.size() ) {
        if ( 1 == affectedFiles.size() ) {
            fullFileName = affectedFiles.first().path
            if ( "version.sbt" == fullFileName.substring(fullFileName.lastIndexOf("/")+1) ) {
                return true
            }
        }
    }
    return false
}

///
def _isOnlyVersionBump() {
    def fullFileName
    if ( 1 == currentBuild.changeSets.size() ) { 
		if ( 2 > currentBuild.changeSets[0].items.size() ) { 
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
                 println _isOnlyVersionBump()
             }
         }
     }
}
