#!groovy
pipeline {
    agent any
    stages {
        stage ('Select module') {
            steps {
               script{
                 def USER_INPUT=input(id: 'USER_INPUT',
                     message: 'stage Selection required',
                     parameters:[
                        [$class   : 'ChoiceParameterDefinition',
                        choices  : ['Regression','Selective Build'].join('\n'),
                        name     : 'USER_INPUT',
                        description:'Select the modules']
                     ])
                 echo "Selected modules are : ${USER_INPUT}"
               }
            }
        }
        stage ('Regression') {
             steps {

                 }
             }
        }
        stage ('Regression') {
                    parallel {
                   // The substages
                           stage('Module1') {
                               steps {

                               }
                           }
                           stage('Module2') {
                               steps {

                               }
                           }
                           stage('module3') {
                               steps {

                               }
                           }
                   }
        }
    }
}