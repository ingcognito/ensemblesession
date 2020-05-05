pipeline {
    agent homelab
    environment {
        CREDENTIALS_ID = credentials('homelab-gcp-jenkins-service-account')	
        BUCKET = 'ensemblecanada-com'
        PATTERN = './*'
    }
    stages {
        stage('Store to GCS') {
	    when {
        	expression { BRANCH_NAME ==~ /master/ }
      	    }
            steps{
                step([$class: 'ClassicUploadStep', 
		credentialsId: env.CREDENTIALS_ID,  
		bucket: "gs://${env.BUCKET}",
                      pattern: env.PATTERN])
            }
        }
    }
}
