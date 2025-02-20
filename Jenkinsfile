pipeline {
    agent any

    stages {
        stage('build') {
            agent {
                docker { 
                    image 'node:18-alpine' 
                    args '--user=root'  // Allow installing packages
                }
            }
            steps {
                sh ''' 
                node --version
                npm --version
                
                # Set npm cache to a writable directory
                npm config set cache /home/node/.npm
                
                # Ensure cache directory is writable
                mkdir -p /home/node/.npm && chmod -R 755 /home/node/.npm
                
                # Remove old dependencies
                rm -rf node_modules package-lock.json

                # Clean npm cache
                npm cache clean --force

                # Install dependencies and build
                npm install
                npm run build
                '''
            }
        }
    }
}
