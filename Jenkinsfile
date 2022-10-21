pipeline {
    agent any 
     stages {
	stage ("Building the docker image") {
		steps {
			script {
				checkout scm
				sh 'rm -rf *.war'
				sh 'jar -cvf 645-assign1.war -C portfolio/src/main/webapp .' 
				sh 'echo $(BUILD_ID}'
			}
		}
	}
	stage("Pushing Image to DockerHub") {
		steps {
			script {
				sh 'docker push koushiksura/645-assign2:${BUILD_TIMESTAMP}'
			}
		}
	}
	
	}
}
