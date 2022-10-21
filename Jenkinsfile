pipeline {
    agent any 
     stages {
	stage ("Building the docker image") {
		steps {
			script {
				checkout scm
				sh 'rmp -rf * war'
				sh 'jar -cvf 645-assign1.war -C portfolio/src/main/webapp .' 
				sh 'echo $(BUILD_TIMESTAMP}'
				sh "docker login -u koushiksura -p ${env.DOCKERHUB_PASS}"
				def customImage = docker.build("koushiksura/645-assign2:${env.BUILD_TIMESTAMP}")
			}
		}
	}
	stage("Pushing Image to DockerHub") {
		steps {
			script {
				sh 'docker push koushiksura/645-assign2:${BUILD_TIMESTAMP}"
			}
		}
	}
	
	}
}
