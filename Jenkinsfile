pipeline {
    agent any

    stages {
        stage('Installing dependencies')  {
            steps {
                sh 'printenv'
                echo "Installing..."
                dir("${env.WORKSPACE}/docusaurus")
                sh "yarn"
            }
        }

        stage('Build')  {
            steps {
                echo "Building..."
                sh "yarn build"
            }
        }

        stage('Deploy') {
            when {
                expression {
                    currentBuild.result == null || currentBuild.result == "SUCCESS"
                }
            }
            steps {
                sh "cp -r ./build/* /var/www/599271.cloud4box.ru/docs/"
            }
        }
    }
}
