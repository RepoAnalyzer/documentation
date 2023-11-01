pipeline {
    agent any

    stages {
        stage('Build')  {
            steps {
                echo "Building..."
                sh 'yarn cwd=docusaurus build'
            }
        }

        stage('Deploy') {
            if (currentBuild.result == null || currentBuild.result == 'SUCCESS') {
                sh 'cp -r docusaurus/build/* /var/www/599271.cloud4box.ru/docs/'
            }
        }
    }
}
