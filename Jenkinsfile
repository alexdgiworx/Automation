pipeline {
  agent any

  environment {
    NETLIFY_SITE_ID = 'nfp_xcow5AqY1FuxrADGezqShj8qvXVZsSKndf50' // 🔁 Replace with your actual site ID from Netlify
    NETLIFY_AUTH_TOKEN = credentials('NETLIFY_TOKEN') // 🔒 Stored in Jenkins > Credentials
  }

  stages {
    stage('Clone Repo') {
      steps {
        git url: 'https://github.com/alexdgiworx/Automation.git', branch: 'main'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Build Vite App') {
      steps {
        sh 'npm run build'
      }
    }

    stage('Deploy to Netlify') {
      steps {
        sh '''
          npm install -g netlify-cli
          netlify deploy --dir=dist --site=$NETLIFY_SITE_ID --auth=$NETLIFY_AUTH_TOKEN --prod
        '''
      }
    }
  }
}
