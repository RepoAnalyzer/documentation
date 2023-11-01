pipeline {
    agent any

    stages {
        stage('Installing dependencies')  {
            steps {
                sh "pwd"
                sh 'printenv'
                echo "Installing..."
                dir("docusaurus") {
                    sh "yarn"
                }
            }
        }

        stage('Build')  {
            steps {
                echo "Building..."
                dir("docusaurus") {
                    sh "yarn build"
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
                dir("docusaurus") {
                    sh "cp -r ./build/* /var/www/599271.cloud4box.ru/docs/"
                }
            }
        }
    }
}
