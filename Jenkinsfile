def isOnlyVersionBump() {
    try {
        // full path file name.
        def fullFileName
        def changeSets = currentBuild.changeSets
        def items = changeSets[0].items
        def affectedFiles = items[0].affectedFiles

		println changeSets.size()
		println items.size()
		println affectedFiles.size()
		
        // single changeSet, single item, single affectedFile
        if ( 1 == changeSets.size() ) {
            if ( 1 == items.size() ) {
                if ( 1 == affectedFiles.size() ) {
                    fullFileName = affectedFiles.first().path
                    if ( "version.sbt" == fullFileName.substring(fullFileName.lastIndexOf("/")+1) ) {
                        return true
                    }
                }
            }
        }
        return false
    } catch (Exception e) {
        return false
    }
}


def _isOnlyVersionBump() {
    def fullFileName
    if ( 1 == currentBuild.changeSets.size() ) { 
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
                 println isOnlyVersionBump()
             }
         }
     }
}
