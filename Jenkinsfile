mvn deploy
scp /root/workspace/build/feature/target/*.war root@172.31.31.24:/opt/apache-tomcat-9.0.55/webapps


pipeline {

	agent { label 'dev-slaves'}
	triggers {
        pollSCM '* * * * *'
                 }
	stages {
	   stage ( 'scm checkout' ) {
		steps { 
			checkout scmGit(branches: [[name: '*/feature1']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/DevOps-Nortek/mavenrepo.git']])
                      }
                                    }
	   stage ( 'build' ) {
		steps {
			sh 'mvn package'
                      }
                             }
	   stage ( 'uploadArtifactory' ) {
		steps {
			sh 'mvn deploy'
		       }
					 }
	   stage ( 'installApplication' ) {
		steps {
			sh 'scp /root/workspace/build/feature/target/*.war root@172.31.31.24:/opt/apache-tomcat-9.0.55/webapps'
		      }
					  }
	   stage ( 'postBuildNotification' ) {
		steps {
			emailext body: '$DEFAULT_CONTENT', subject: '$DEFAULT_SUBJECT', to: 'chandu3393@gmail.com, nayakchandu1994@gmail.com'
		      }
					     }
               }
}
