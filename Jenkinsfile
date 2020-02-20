#!/bin/env groovy

node {
    deleteDir()
    checkout scm
    files = sh(returnStdout: true, script: 'ls')
    println "list of property files"
    p_files = files.split("\n").collect()[2,3]
    sh 'ls -la'
    
    sh 'ls | grep prop >> file_p'
    sh 'ls -la'


    liste1 = readFile 'file_p'

	//liste2 = 'if(liste1.equals(p_files[0])){return p_files[0].readLines()} else if(liste1.equals(p_files[1])){return p_files[1].readLines()}'
	
	
	if (liste1.equals(p_files[0])){
		liste2 = readFile p_files[0]
	} else {
		liste2 = readFile p_files[1]
	}
	
	/*
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
		 	choices: "${liste2}",
		 	description: 'select another choice : ',
		 	name: 'choice2'
			]
		]
		]
    ])
	*/
	properties([
        parameters([
            [$class: 'ChoiceParameter',
				choiceType: 'PT_SINGLE_SELECT',
				description: 'Select file',
				filterLength: 1,
				filterable: false,
				name: 'Files',
				randomName: 'choice-parameter-5631314439613978',
				script: [
					$class: 'GroovyScript', 
					fallbackScript: [
						classpath: [],
						sandbox: false,
						script: ''
					],
					script: [
						classpath: [],
						sandbox: false,
						script: 'return['${p_files[0]}','${p_files[1]}']'
					]
				]
			],
			[$class: 'CascadeChoiceParameter',
				choiceType: 'PT_SINGLE_SELECT',
				description: 'Select value from file',
				filterLength: 1,
				filterable: false,
				name: 'Value',
				randomName: 'choice-parameter-5631314456178619',
				referencedParameters: 'files',
				script: [
					$class: 'GroovyScript',
					fallbackScript: [
						classpath: [],
						sandbox: false,
						script: ''
					],
					script: [
						classpath: [],
						sandbox: false,
						script: sh(returnStdout: true, script: 'echo ${liste2}')
					]
				]
			]
		])
])
    sh 'echo Hello World'

}
