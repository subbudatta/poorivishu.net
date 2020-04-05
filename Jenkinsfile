
pipeline {
   agent any
   stages{
   stage('Checkout or pull from github'){
       steps{
       git credentialsId: '7ad45fba-8f01-467b-ab99-d0c0520c9e5d', url: 'https://github.com/poornimayo/helloworld.git'
       } 
   }
   stage('clean and install dependecies'){
   steps{
   bat label: '', script: 'mvn clean install'
   }
   }
      stage('compile'){
            steps{
               bat label: '', script: '''mvn compile

'''
            }
            }
               
   stage('build'){
       steps{
       bat label: '', script: '''mvn clean package
'''
       }
   }
   stage('unit testing')
   {
       steps{
       bat label: '', script: '''mvn test
'''
       }
   }
   stage('run')
   {
       steps{
       bat label: '', script: '''mvn verify

'''
       }
   }
    stage('deploy or deliver to test server'){
         steps{
              deploy adapters: [tomcat9(credentialsId: 'b63ce927-d2f5-46b4-916f-31702814f93d', path: '', url: 'http://localhost:8088/')], contextPath: 'login', war: '**/*.war'
         }
      }
       stage('cucumber report'){
          steps{
             cucumber failedFeaturesNumber: -1, failedScenariosNumber: -1, failedStepsNumber: -1, fileIncludePattern: '**/*.json', pendingStepsNumber: -1, skippedStepsNumber: -1, sortingMethod: 'ALPHABETICAL', undefinedStepsNumber: -1 
          }
      }
}
}
