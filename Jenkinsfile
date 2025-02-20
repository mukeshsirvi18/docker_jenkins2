pipeline {
    agent any

    stages {
        stage('build') {
            agent {
                docker { 
                    image 'node:18-alpine' 
                    args '--user 1000:1000'  // Run container as a non-root user
                }
            }
            steps {
                sh ''' 
                node --version
                npm --version
                
                # Set npm cache to a safe directory
                npm config set cache ~/.npm

                # Ensure cache directory is writable
                mkdir -p ~/.npm && chmod -R 755 ~/.npm

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
