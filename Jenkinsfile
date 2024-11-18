pipeline {
    agent any

    environment {
        REPO_URL = "http://${env.MAVEN_URL}/repository/maven-snapshots/"
        REPO_ID = "maven-snapshots"
    }

    tools {
        maven 'M3'
    }

    stages {
        stage('构建并发布') {
            steps {
                script {
                    dir('cloud-parent') {
                        sh "mvn clean deploy -DaltDeploymentRepository=${REPO_ID}::default::${REPO_URL}"
                    }

                    dir('service-parent') {
                        sh "mvn clean deploy -DaltDeploymentRepository=${REPO_ID}::default::${REPO_URL}"
                    }
                }
            }
        }
    }
}