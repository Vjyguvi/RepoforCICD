pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh 'docker build -t my-flask2 .'
        sh 'docker tag my-flask2 $dockertag'
      }
    }
    stage('Test') {
      steps {
        sh 'docker run -d -it --name appserver2 -p3001:5000 my-flask'
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
            emailext body: 'From Jenkins Job', subject: 'Jenkins RunTime', to: 'aws.vjy@gmail.com'
        }
}

}

             
              
  

                 
    
  
    

  

