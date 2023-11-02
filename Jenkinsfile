pipeline {
    agent any

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
                    sh "REACT_APP_WWW_LOCATION=${env.GIT_BRANCH}"
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
            steps {
                fileOperations {
                    folderCreateOperation("var/www/599271.could4box.ru/docs/${env.GIT_BRANCH}")
                }
                dir("docusaurus") {
                    sh "cp -r ./build/* /var/www/599271.cloud4box.ru/docs/${env.GIT_BRANCH}"
                }
            }
        }
    }
}
