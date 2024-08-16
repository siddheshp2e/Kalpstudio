pipeline {
	agent any
	options {
        skipStagesAfterUnstable()
		timeout(time: 30, unit: 'MINUTES')
    	}
	environment {
		STG_ECR_URL = '408153089286.dkr.ecr.ap-south-1.amazonaws.com/kalp-studio-doc-stg'
		STG_ENV = 'stg'
		SLACK_CHANNEL = 'pl-builds-alerts'
    }
	stages {
		stage('STG_BUILD') {
			when{
				branch 'stage'
			}
			steps {
				script {
					committerEmail = sh (
      				script: 'git log -1 --pretty=format:"%an"',
      				returnStdout: true
					).trim()
				}
				echo "Committer Email : '${committerEmail}'"
				slackSend (	color: 'good', channel: "${SLACK_CHANNEL}", message: "${env.JOB_NAME} | Job has initiated : #${env.BUILD_NUMBER} by ${committerEmail}")
				slackSend (	color: 'warning', channel: "${SLACK_CHANNEL}", message: "${env.JOB_NAME} | Build is started : #${env.BUILD_NUMBER}")
				sh "aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 408153089286.dkr.ecr.ap-south-1.amazonaws.com"
				echo "Step: BUILD, initiated..."
				sh "aws ecr get-login --no-include-email --region ap-south-1 | sh"
				sh "docker build -t '${STG_ECR_URL}':'${BUILD_NUMBER}' . --no-cache"
				slackSend ( color: 'warning', channel: "${SLACK_CHANNEL}", message: "${env.JOB_NAME} | Build has been completed : #${env.BUILD_NUMBER}")
			}
		}
		stage('STG_ECR PUSH') {
			when{
				branch 'stage'
			}
			steps {
				echo "Step: Pushing Image ..."
				sh "aws ecr get-login --no-include-email --region ap-south-1 | sh"
				sh "docker push '${STG_ECR_URL}':${BUILD_NUMBER}"
           			slackSend ( color: 'warning', channel: "${SLACK_CHANNEL}", message: "${env.JOB_NAME} | Build has been pushed to the ECR : #${env.BUILD_NUMBER}")
			}
		}
		stage('STG_DEPLOY') {
			when{
				branch 'stage'
			}
			steps {
				echo "Deploying into '${STG_ENV}' environment"
				sh "aws eks --region ap-south-1 update-kubeconfig --name p2epro-stg"
				sh "sed -i 's/<VERSION>/${BUILD_NUMBER}/g' deployment-'${STG_ENV}'.yaml"
				sh "kubectl apply -f deployment-'${STG_ENV}'.yaml"
				echo "'${STG_ENV}' deployment completed: '${env.BUILD_ID}' on '${env.BUILD_URL}'"
           			slackSend (	color: 'warning', channel: "${SLACK_CHANNEL}", message: "${env.JOB_NAME} | Deployment has been completed : #${env.BUILD_NUMBER}")
			}
		}
		stage('POST_CHECKS') {
			when{
				expression {
                   	env.BRANCH_NAME == 'development' || env.BRANCH_NAME == 'qa' || env.BRANCH_NAME == 'stage'
                }
			}
			steps {
				echo "POST test"
			}
			post {
				always {
					echo "ALWAYS test1"
				}
				success {
					slackSend (	color: 'good', channel: "${SLACK_CHANNEL}", message: "${env.JOB_NAME} | Job has succeeded : #${env.BUILD_NUMBER} in ${currentBuild.durationString.replace(' and counting', '')} \n For more info, please click (<${env.BUILD_URL}|here>)")
			        echo "Good to deploy into STG"
				}
				failure {
					slackSend (	color: 'danger', channel: "${SLACK_CHANNEL}", message: "${env.JOB_NAME} | @channel - Job has failed #${env.BUILD_NUMBER}\nPlease check full info, (<${env.BUILD_URL}|here>)")
				}
			}
		}
	}
	post {
		always {
			echo "ALWAYS last-post check"
		}
		aborted {
			slackSend (
				color: '#AEACAC', channel: "${SLACK_CHANNEL}", message: "${env.JOB_NAME} | Job has aborted : #${env.BUILD_NUMBER} in ${currentBuild.durationString.replace(' and counting', '')} \n For more info, please click (<${env.BUILD_URL}|here>)")
		}
		failure {
			slackSend (
				color: 'danger', channel: "${SLACK_CHANNEL}", message: "${env.JOB_NAME} | @channel - Job has failed #${env.BUILD_NUMBER}\nPlease check full info, (<${env.BUILD_URL}|here>)")
		}
	}
}
