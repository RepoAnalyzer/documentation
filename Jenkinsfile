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
            when {
                expression {
                    currentBuild.result == null || currentBuild.result == 'SUCCESS'    
                }
            }
            steps {
                sh 'cp -r docusaurus/build/* /var/www/599271.cloud4box.ru/docs/'
            }
        }
    }
}
