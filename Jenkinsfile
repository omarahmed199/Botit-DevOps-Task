pipeline {

    agent any

    stages{
        stage('Build') {
          steps {
            script {
              withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) { 

              sh """
                 docker build .  -t omarkorety/botit:V${BUILD_NUMBER}
                echo ${BUILD_NUMBER}
                 docker login -u ${USERNAME} -p ${PASSWORD}
                docker push omarkorety/botit:V${BUILD_NUMBER}
                echo ${BUILD_NUMBER} > ../build_num.txt
                """
                    }
                        } 
                }
            }
    

        stage('Deploy') {
          steps{
            script {
                 
                            sh """

                              docker run -d -p 5000:5000 --name task omarkorety/botit:V${BUILD_NUMBER}
                            """

                }

              }
            
          }
        }

}

        

