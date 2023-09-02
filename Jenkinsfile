node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        def gitUrl = "https://github.com/${env.GIT_USERNAME}/projectpipeline5_manf.git"
                        sh "git config user.email prashantjkamath@gmail.com"
                        sh "git config user.name prashantjkamath"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+prashantjkamath/pythonapp5.*+prashantjkamath/pythonapp5:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push ${gitUrl} HEAD:main"
      }
    }
  }
}
}