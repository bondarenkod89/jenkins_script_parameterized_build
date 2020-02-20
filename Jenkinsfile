#!/bin/env groovy

node {
    deleteDir()
    checkout scm
    files = sh(returnStdout: true, script: 'ls')
    println "list of property files"
    p_files = files.split("\n").collect()[2,3]
    sh 'ls -la'
    
    fileprop = sh (returnStdout: true, script: 'ls | grep prop > file_p')
    sh 'ls -la'


    liste1 = readFile 'file_p'
	
	if (liste1.equals(file_p[0])){
		liste2 = readFile file_p[0]
	} else {
		liste2 = readFile file_p[1]
	}
    
//    liste2 = readFile 'property2'
	
	properties(
    [
        [$class: 'ParametersDefinitionProperty',
		parameterDefinitions: [
			[$class: 'ChoiceParameterDefinition',
			 choices: "${liste1}",
			 description: 'select your choice : ',
			 name: 'choice1'
			],
        	[$class: 'ChoiceParameterDefinition',
		 	choices: '${liste2}',
		 	description: 'select another choice : ',
		 	name: 'choice2'
			]
		]
		]
    ])

    sh 'echo Hello World'

}
