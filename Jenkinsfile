#!/bin/env groovy

node {
    deleteDir()
    checkout scm
    files = sh(returnStdout: true, script: 'ls')
    println "list of property files"
    println files.split("\n").collect()[2,3]
    sh 'ls -la'
    
    fileprop = sh (returnStdout: true, script: 'ls | grep prop > fileproperty')
    sh 'ls -la'

    liste1 = readFile 'fileproperty'
    liste2 = readFile 'property2'
	
    properties(
    [
        [
                $class              : 'ParametersDefinitionProperty',
                parameterDefinitions: [
                        [
                                $class     : 'ChoiceParameterDefinition',
                                choices    : "${liste1}",
                                description: 'select your choice : ',
                                name       : 'choice1'
                        ],
                        [
                                $class     : 'ChoiceParameterDefinition',
                                choices    : '',
                                description: 'select another choice : ',
                                name       : 'choice2'
                        ]
		]
	]
    ])

    sh 'echo Hello World'

}
