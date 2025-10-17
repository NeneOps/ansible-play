pipeline {
    agent any
    
    stages {
        stage('Create a Zip File') {
            steps {
                script {
                    // Define the name of the zip file
                    def zipFileName = "play.zip"
                    
                    // Create a zip file containing all files in the workspace
                    sh "zip -r ${zipFileName} ."
                    
                    // Send the zip file to JFrog Artifactory
                    //archiveArtifacts artifacts: zipFileName, fingerprint: true
                }
            }
            
        }
        stage('Upload to Artifactory') {
                steps {
                    script {  // Define Artifactory server and repository details
                      sh  ''' curl -uadmin:AP7iKibFPukTLYzjaqQWMbvj12T -T play.zip \
                        "http://54.242.136.171:8081/artifactory/Ansible-repo/plays/play.zip" '''
                        }
                      

                }
             }
             stage('Download from Artifactory to Ansible Server'){
                steps {
                    sh "curl -uadmin:AP7iKibFPukTLYzjaqQWMbvj12T -O \
                    "http://54.242.136.171:8081/artifactory/Ansible-repo/plays/play.zip" "
                }
             }
             

    }
}