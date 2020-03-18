pipeline{

    agent any

    stages {

        stage ('Compile Stage') {

            steps {

                withMaven(maven: 'maven_3_5_0') {
                    sh 'mvn clean install'
					sh 'ls'
					sh 'pwd'

                }

            }
        }
    stage ('Test Stage') {

            steps {

                withMaven(maven: 'maven_3_5_0') {
                    sh 'mvn test'
					

                }

            }
        }


        stage ('Cucumber Reports') {

            steps {
                cucumber buildStatus: "UNSTABLE",
                    fileIncludePattern: "**/cucumber.json",
                    jsonReportDirectory: 'target'
					sh 'ls'
					sh 'pwd'
					sh 'ls target'

            }

        }

    }
	
	 post {
        failure {
            emailext attachmentsPattern: 'target/cucumber.json', body: "Job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) failed", 
                    subject: "${env.JOB_NAME} - Build # ${env.BUILD_NUMBER} - Failed", 
                    mimeType: 'text/html',to: "avinash.karimikonda@accoliteindia.com"
            }
         success {
               emailext attachmentsPattern: '/var/lib/jenkins/jobs/cucu/builds/14/cucumber-html-reports/overview-features.html', body: "Job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) success.", 
                    subject: "${env.JOB_NAME} - Build # ${env.BUILD_NUMBER} - Successful", 
                    mimeType: 'text/html',to: "avinash.karimikonda@accoliteindia.com"
          }      
    }

}