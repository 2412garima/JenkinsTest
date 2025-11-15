pipeline {
    agent any

    stages {
        stage('FirstStep') {
            steps {
                echo "Jenkins job ran on commit"
            }
        }

    }

    post {
        always {
            echo "Jenkins job completed"
        }
    }
}
