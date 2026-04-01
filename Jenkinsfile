pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // GitHub에서 코드를 가져옵니다.
                checkout scm
            }
        }

        stage('Permission') {
            steps {
                // 맥/리눅스 환경에서 gradle 실행 권한을 부여합니다.
                sh 'chmod +x gradlew'
            }
        }

        stage('Build') {
            steps {
                // 프로젝트를 빌드하고 jar 파일을 생성합니다.
                sh './gradlew clean build'
            }
        }

        stage('Test') {
            steps {
                // 테스트 코드를 실행합니다.
                sh './gradlew test'
            }
        }
    }

    post {
        success {
            // 빌드 성공 시 생성된 jar 파일을 젠킨스에 보관합니다.
            archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            echo 'Build and Test Finished Successfully!'
        }
    }
}
