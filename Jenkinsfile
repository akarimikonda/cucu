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
					sh "cp /var/lib/jenkins/jobs/cucu/builds/${env.BUILD_NUMBER}/cucumber-html-reports/overview-features.html target/"

            }

        }

    }
	
	 post {
        failure {
            emailext attachmentsPattern: 'target/cucumber.json', body: '${FILE, path="myfile.html"}', 
                    subject: "${env.JOB_NAME} - Build # ${env.BUILD_NUMBER} - Failed", 
                    mimeType: 'text/html',to: "avinash.karimikonda@accoliteindia.com"
            }
         success {
               emailext attachmentsPattern: 'target/overview-features.html', body: '${FILE, path="target/overview-features.html"}', 
                    subject: "${env.JOB_NAME} - Build # ${env.BUILD_NUMBER} - Successful", 
                    mimeType: 'text/html',to: "avinash.karimikonda@accoliteindia.com"
          }      
    }

}