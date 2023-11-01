pipeline {
    agent any

    stages {
        stage('Build')  {
            steps {
                sh 'printenv'
                echo "Building..."
                sh 'yarn cwd=${env.WORKSPACE}/docusaurus build'
            }
        }

        stage('Deploy') {
            when {
                expression {
                    currentBuild.result == null || currentBuild.result == 'SUCCESS'    
                }
            }
            steps {
                sh 'cp -r ${env.WORKSPACE}/docusaurus/build/* /var/www/599271.cloud4box.ru/docs/'
            }
        }
    }
}
