node {
    def app
    
    env.IMAGE = 'josepht05/bluegreen-rollout-july'

    stage('Clone repository') {
             git branch: 'main', url: 'https://github.com/taiwoj14/rollout-manifests.git'  
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'taiwo-github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //script {def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')}
                        sh "git config user.email twin1405j@gmail.com"
                        sh "git config user.name taiwoj14"
                        //sh "git switch master"
                        sh "cat rollout.yml"
                        sh "sed -i 's+${IMAGE}.*+${IMAGE}:${DOCKERTAG}+g' rollout.yml"
                        sh "cat rollout.yml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job Rolloutmanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/rollout-manifests.git HEAD:main"
                      
             }
         }
     }
  }
}
