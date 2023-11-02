pipeline {
    agent any

    environment {
        SITE = 'http://599271.cloud4box.ru/docs'
    }

    stages {
        stage('Installing dependencies')  {
            steps {
                sh "pwd"
                sh 'printenv'
                echo "Installing..."
                dir("docusaurus") {
                    yarn 'install'
                }
            }
        }

        stage('Build')  {
            steps {
                echo "Building..."
                dir("docusaurus") {
                    fileOperations([
                        fileCreateOperation(fileName: ".env", fileContent: "DOCUSAURUS_WWW_LOCATION=${env.GIT_BRANCH}")
                    ])
                    yarn 'build'
                }
            }
        }

        stage('Deploy') {
            when {
                expression {
                    currentBuild.result == null || currentBuild.result == "SUCCESS"
                }
            }
            environment {
                SITE_BASE_LOCATION = '/var/www/599271.cloud4box.ru/docs'
            }
            steps {
                fileOperations([
                    folderCreateOperation("${SITE_BASE_LOCATION}/${env.GIT_BRANCH}")
                ])
                dir("docusaurus") {
                    sh "cp -r ./build/* ${SITE_BASE_LOCATION}/${env.GIT_BRANCH}"
                }
            }
        }
    }

	post {
		success {
            publishChecks name: 'Deployment', title: 'Deployment',
                summary: "Open [url](${SITE}/${env.GIT_BRANCH}) to see deployed docs",
                detailsURL: "${env.RUN_DISPLAY_URL}"
		}
	}
}
