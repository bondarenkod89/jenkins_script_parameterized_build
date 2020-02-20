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
						script: sh(returnStdout: true, script: 'cat ./fileproperty')
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
						script: sh(returnStdout:true, script: 'cat ./property2')
					]
				]
			]
		])
    ])

    sh 'echo Hello World'

}
