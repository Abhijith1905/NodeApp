node {
    def app

    stage('Clone repository') {
        // Cloning the Repository to our Workspace
        checkout scm
    }

    stage('Build image') {
        // This builds the actual image
        app = docker.build("abhijithkora2005/nodeapp")
    }

    stage('Test image') {
        script {
            docker.image("abhijithkora2005/nodeapp").inside("/c/ProgramData/Jenkins/.jenkins/workspace/Docker-Pipeline/") {
                sh 'npm test'  // Replace with your test command
            }
        } // Closing script block
    } // Closing Test image stage

    stage('Push image') {
        // You need to register with DockerHub before you can push images to your account
        docker.withRegistry('https://registry.hub.docker.com', 'new-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
        echo "Trying to Push Docker Build to DockerHub"
    }
} // Closing node block
