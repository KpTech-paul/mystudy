pipeline { 
    agent any 
 
    stages { 
        stage('Checkout') { 
            steps { 
                echo 'Downloading HTML source code' 
                checkout scm 
            } 
        } 
 
        stage('Build') { 
            steps { 
                echo 'Checking HTML project files' 
                bat 'dir' 
            } 
        } 
 
        stage('Docker Build') { 
            steps { 
                echo 'Building Docker image' 
                bat 'docker build -t mystudy:latest .' 
            } 
        } 
 
        stage('Deploy') { 
            steps { 
                echo 'Deploying HTML website' 
                bat ''' 
                docker rm -f mystudy 2>NUL 
                docker run -d --name mystudy -p 8083:80 mystudy:latest 
                ''' 
            } 
        } 
    } 
 
    post { 
        success { 
            echo 'Website deployed successfully!' 
        } 
        failure { 
            echo 'Deployment failed. Check the console output.' 
        } 
    } 
} 