#!/bin/env groovy

node {
    deleteDir()
    checkout scm
    files = sh(returnStdout: true, script: 'ls')
    println "list of property files"
    p_files = files.split("\n").collect()[2,3]
    sh 'ls -la'
    
    test1 = sh(returnStdout:true, script: "cat ${p_files[0]}")
    sh 'echo "----------------------------------------------"'
    test2 = sh(returnStdout:true, script: "cat ${p_files[1]}")

    sh 'ls | grep prop >> file_list'
    sh '''sed "s/.*/'&',/" file_list > temp1'''
    sh '''sed '$ s/,$//' temp1 > file_list'''
    sh '''sed ''1' s/^/return[/\n' file_list > temp1'''
    sh '''echo "]" >> temp1 && mv temp1 file_list'''
    
    sh 'ls -la'
    sh 'cat ./file_list'
    
    if (files.equals(p_files[0])){
        sh '''sed "s/.*/'&',/" ${p_files[0]} > property_list'''
        sh '''sed '$ s/,$//' property_list > temp2'''
        sh '''sed ''1' s/^/return[/\n' temp2 > property_list'''
        sh '''echo "]" >> property_list'''
//        sh '''sed "s/.*/'&',/" ${p_files[0]} > temp1 | sed '$ s/,$//' temp1 > property_list'''
    } else {
        sh '''sed "s/.*/'&',/" ${p_files[1]} > property_list'''
        sh '''sed '$ s/,$//' property_list > temp2'''
        sh '''sed ''1' s/^/return[/\n' temp2 > property_list'''
        sh '''echo "]" >> property_list'''
//        sh '''sed "s/.*/'&',/" ${p_files[1]} > temp1 | sed '$ s/,$//' temp1 > property_list'''
    }
    
    properties([
        parameters([
            [$class: 'ChoiceParameter',
            choiceType: 'PT_SINGLE_SELECT',
            description: 'Select file',
            filterLength: 1,
            filterable: false,
            name: 'Files',
            randomName: 'choice-parameter-5631314439613978',
            script: 
                [$class: 'GroovyScript', 
                fallbackScript: [
                    classpath: [],
                    sandbox: false,
                    script: ''
                ],
                script: [
                    classpath: [],
                    sandbox: false,
                    script: sh(returnStdout:true, script: 'cat ./file_list')

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
            script: 
                [$class: 'GroovyScript',
                fallbackScript: [
                    classpath: [],
                    sandbox: false,
                    script: ''
                ],
                script: [
                    classpath: [],
                    sandbox: false,
                    script: sh(returnStdout:true, script: 'cat ./file_list')
                ]
                ]
            ]
        ])
    ])
    sh 'echo Hello World'

}
