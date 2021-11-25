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
                        choices  : ['ABC','DFE','XYZ'].join('\n'),
                        name     : 'USER_INPUT',
                        description:'Select the modules']
                     ])
                 echo "Selected modules are : ${USER_INPUT}"
               }
            }
        }
        stage ('Testing Stage') {
             steps {
                 withMaven(maven : 'apache-maven-3.6.1') {
                      bat 'mvn test'
                 }
             }
        }
    }
}