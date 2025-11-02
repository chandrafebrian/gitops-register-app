// pipeline {
//     agent { label "jenkins-agent" }
//     environment {
//               APP_NAME = "register-app-pipeline"
//     }

//     stages {
//         stage("Cleanup Workspace") {
//             steps {
//                 cleanWs()
//             }
//         }

//         stage("Checkout from SCM") {
//                steps {
//                    git branch: 'main', credentialsId: 'github-chandra', url: 'https://github.com/chandrafebrian/gitops-register-app'
//                }
//         }

//         stage("Update the Deployment Tags") {
//             steps {
//                 sh """
//                    cat deployment.yaml
//                    sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
//                    cat deployment.yaml
//                 """
//             }
//         }

//         stage("Push the changed deployment file to Git") {
//             steps {
//                 sh """
//                    git config --global user.name "chandrafebrian"
//                    git config --global user.email "chandrafebrian99@gmail.com"
//                    git add deployment.yaml
//                    git commit -m "Updated Deployment Manifest"
//                 """
//                 withCredentials([gitUsernamePassword(credentialsId: 'github-chandra', gitToolName: 'Default')]) {
//                   sh "git push https://github.com/chandrafebrian/gitops-register-app main"
//                 }
//             }
//         }
      
//     }
// }


pipeline {
    agent { label "jenkins-agent" }
    environment {
              APP_NAME = "register-app-pipeline"
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }

        stage("Checkout from SCM") {
               steps {
                   git branch: 'main', credentialsId: 'github-chandra', url: 'https://github.com/chandrafebrian/gitops-register-app'
               }
        }

        stage("Update the Deployment Tags") {
            steps {
                sh """
                   cat deployment.yaml
                   sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
                   cat deployment.yaml
                """
            }
        }

        stage("Push the changed deployment file to Git") {
            steps {
                sh """
                   git config --global user.name "chandrafebrian"
                   git config --global user.email "chandrafebrian99@gmail.com"
                   git add deployment.yaml database.yaml
                   git commit -m "Updated Deployment Manifest and database manifest" || echo "No changes to commit"
                """
                withCredentials([gitUsernamePassword(credentialsId: 'github-chandra', gitToolName: 'Default')]) {
                  sh "git push https://github.com/chandrafebrian/gitops-register-app main"
                }
            }
        }
      
    }
}