node {
    def app
    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        when {
            branch 'dev'  // Only build on the 'dev' branch
        }
        steps {
            script {
                app = docker.build("imosh/kiii")
            }
        }
    }

    stage('Push image') {   
        when {
            branch 'dev'  // Only push on the 'dev' branch
        }
        steps {
            script {
                docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                    app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                    app.push("${env.BRANCH_NAME}-latest")
                }
            }
        }
    }
}

