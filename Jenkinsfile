pipeline {
  agent any

  environment {
    NETLIFY_SITE_ID = 'nfp_xcow5AqY1FuxrADGezqShj8qvXVZsSKndf50' // Paste from Netlify Site Settings
  }

  stages {
    stage('Checkout Latest Code') {
      steps {
        git url: 'https://github.com/alexdgiworx/Automation.git', branch: 'main'
      }
    }

    stage('Install Dependencies') {
      steps {
        bat 'npm install'
      }
    }

    stage('Build Vite App') {
      steps {
        bat 'npm run build'
      }
    }

    stage('Deploy to Netlify') {
      steps {
        withCredentials([string(credentialsId: 'NETLIFY_TOKEN', variable: 'TOKEN')]) {
          bat '''
            set PATH=%APPDATA%\\npm;%PATH%
            netlify deploy --dir=dist --site=%NETLIFY_SITE_ID% --auth=%TOKEN% --prod
          '''
        }
      }
    }
  }
}
