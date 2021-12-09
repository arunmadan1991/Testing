#!groovy
pipeline {
    agent any
    stages {
        stage ('Testing Selection') {
            steps {
               script{
			        env.Selection =""
			        env.List_Module =[]
			        env.SelectedModule =""
                    def USER_INPUT=input(id: 'USER_INPUT',
                     message: 'stage Selection required',
                     parameters:[
                        [$class   : 'ChoiceParameterDefinition',
                        choices  : ['Regression','Module Selection'].join('\n'),
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
        stage ('Module Selection ') {
              when {
                  allOf{
                 	  expression {"$Selection"== "Module Selection"}
                  }
              }
              steps {
                 script{
              	     env.Selection =""
                         def List_Module = input(id: 'chooseOptions',
                         message: 'Module Selection required',
                         parameters:[
                         [$class   : 'BooleanParameterDefinition',defaultValue : false, name : 'Module1'],
                         [$class   : 'BooleanParameterDefinition',defaultValue : false, name : 'Module2'],
                         [$class   : 'BooleanParameterDefinition',defaultValue : false, name : 'Module3']
                         ])
                         echo "Selected modules are : ${List_Module}"
              		     env.ModulesSelected = "${List_Module}"
              		     env.SelectedModule = "True"
                 }
              }
        }
        stage ('Selected Module Build') {
		     when {
		        allOf{
		          expression {"$SelectedModule"== "True"}
		        }
		     }
             parallel {
             // The substages
                     stage('Module1') {
                          when {
                            allOf{
                               expression {env.ModulesSelected.contains(Module1)}
                            }
                          }
                          steps {
							   echo 'This build for Module1'
						  }
                     }
                     stage('Module2') {
                          when {
                            allOf{
                               expression {env.ModulesSelected.contains(Module2)}
                            }
                          }
                          steps {
						      echo 'This build for Module2'
					      }
                     }
                     stage('Module3') {
                          when {
                            allOf{
                                expression {env.ModulesSelected.contains(Module3)}
                            }
                          }
                          steps {
							   echo 'This build for Module3'
					      }
                     }
             }
        }
    }
}