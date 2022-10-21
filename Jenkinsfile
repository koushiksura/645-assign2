pipeline {
    agent any
     
     stages {
	stage ("Building the docker image") {
		steps {
			script {
				checkout scm
				sh 'rm -rf *.war'
				sh 'jar -cvf 645-assign1.war -C portfolio/src/main/webapp .' 
				sh 'echo ${BUILD_TIMESTAMP}'
 				sh "docker login -u koushiksura -p ${DOCKERHUB_PASSWORD}"
				def customImage = docker.build("koushiksura/645-assign2:${BUILD_NUMBER}")
			}
		}
	}
	stage("Pushing Image to DockerHub") {
		steps {
			script {
				sh 'docker push koushiksura/645-assign2:${BUILD_NUMBER}'
			}
		}
	}
	     stage ("Deploying to Rancher as single pod") {
		steps {
			sh 'kubectl set image deployment/assignment2-645 container-0=koushiksura/645-assign2:${BUILD_NUMBER} -n default'
		}
	}
	stage("Deploying to Rancher as with load balancer") {
		steps {
			sh 'kubectl set image deployment/studentsurvey645-lb studentsurvey645-lb=hekme5/studentsurvey:${BUILD_TIMESTAMP} -n Jenkins-pipeline'
		}
	}
	
	}
}
