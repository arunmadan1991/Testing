#!groovy
pipeline {
    agent any
    stages {
        stage ('Select module') {
            steps {
               script{
			        env.Selection =""
                    def USER_INPUT=input(id: 'USER_INPUT',
                     message: 'stage Selection required',
                     parameters:[
                        [$class   : 'ChoiceParameterDefinition',
                        choices  : ['Regression','Selective Build'].join('\n'),
                        name     : 'USER_INPUT',
                        description:'Select the modules']
                    ])
                 echo "Selected modules are : ${USER_INPUT}"
				 env.Selection = "${USER_INPUT}"
               }
            }
        }
        stage ('Regression') {
		when {
		    allOf{
		      expression {"$Selection"== "Regression"}
		    }
		 }	
          parallel {
                   // The substages
                           stage('Module1') {
                              steps {
							      echo 'This build for module1'
							  }
                           }
                           stage('Module2') {
                               steps {
							      echo 'This build for module2'
							  }
                           }
                           stage('module3') {
                                steps {
							      echo 'This build for module3'
							  }
                           }
                   }  
        }

        stage ('Selective Build') {
		when {
		    allOf{
		      expression {"$Selection"== "Selective Build"}
		    }
		 }
                    parallel {
                   // The substages
                           stage('Module1') {
                               steps {
							      echo 'This build for module1'
							  }
                           }
                           stage('Module2') {
                               steps {
							      echo 'This build for module2'
							  }
                           }
                           stage('module3') {
                                steps {
							      echo 'This build for module3'
							  }
                           }
                    }
        }
    }
}