pipeline {
    agent {
    	label 'homelab'
    }
    environment {
        BUCKET = 'ensemblecanada-com'
    }
    stages {
        stage('Activate Service Account') {
	    when {
        	expression { BRANCH_NAME ==~ /master/ }
      	    }
            steps{
            	withCredentials([file
		(credentialsId: 'homelab-gcp-jenkins-service-account', 
		variable: 'GC_KEY')]) {
    	    	sh("gcloud auth activate-service-account --key-file=${GC_KEY}")}
        	}
    	    }
        stage('Store to GCS') {
	    when {
        	expression { BRANCH_NAME ==~ /master/ }
      	    }
            steps{
	    	sh "gsutil -r cp ./ gs://${env.BUCKET}"
        	}
    	    }
    }
}
