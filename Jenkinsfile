import java.nio.file.*;

@NonCPS
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
    currentBuild.getBuildCauses().toString()
}

node {
   checkout(scm)
   def aci = last_change_sets()
   if ( (new File("dir1")).isDirectory() ) {
      println "it is a directory"
   }
   echo get_cause()
   sh 'echo Done'
   sh 'ls -la'
   // boolean isDir = pFile.isDirectory()
}

