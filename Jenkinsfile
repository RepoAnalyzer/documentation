pipeline {
    agent any

    environment {
        SITE = '599271.cloud4box.ru/docs'
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
            publishChecks name: 'test', title: 'Pipeline Check', summary: 'check through pipeline',
                text: 'you can publish checks in pipeline script',
                detailsURL: 'https://github.com/jenkinsci/checks-api-plugin#pipeline-usage',
                actions: [[label:'an-user-request-action', description:'actions allow users to request pre-defined behaviours', identifier:'an unique identifier']]
		}
	}
}
