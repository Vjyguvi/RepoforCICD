pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh 'docker build -t my-flask1 .'
        sh 'docker tag my-flask1 $dockertag'
      }
    }
    stage('Test') {
      steps {
        sh 'docker run -d -it --name appserver1 -p3000:5000 my-flask'
      }
    }
    stage('Deploy') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerpass', passwordVariable: 'dpassword', usernameVariable: 'dusername')]) {
          sh "docker login -u $dusername -p $dpassword"
          sh 'docker push $dockertag'
        }
      }
    }
    
  }

post{
      always{
            emailext attachLog: true, body: 'From Jenkins Job', compressLog: true, subject: 'Jenkins RunTime', to: 'aws.vjy@gmail.com'
        }
}

}

             
              
  

                 
    
  
    

  

