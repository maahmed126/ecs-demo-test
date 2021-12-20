pipeline {
	triggers {
        upstream(upstreamProjects: 'MasterUpstream',threshold: hudson.model.Result.SUCCESS)//UNSTABLE, FAILURE, NOT_BUILT, ABORTED
    }	
    }			
  agent {
    label 'ecs'
  }
  stages {
    stage('Awesomeness') {
      steps {
        echo 'Hello from Jenkins slave!'
        touch test.txt
      }
    }
  }
  
  post {

		always {
		    sh '''pwd
		        touch test.txt
                ls -l'''
            archiveArtifacts artifacts: '**/*.txt', allowEmptyArchive: true, fingerprint: true
		    // s3CopyArtifact buildSelector: lastSuccessful(), excludeFilter: '', filter: 'test.txt', flatten: false, optional: false, projectName: 'ecs-demo-test', target: '/home/jenkins/workspace/ecs-demo-test'
		}
  }

}
