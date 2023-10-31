pipeline {
    agent { label "linux" }
    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: '', atrifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')
        disableConcurrentBuilds()
    }
    stages {
        stage('Hello')  {
            steps {
                echo "hello jenkins"
            }
        }
    }
}
