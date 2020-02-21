#!/bin/env groovy

node {
    deleteDir()
    checkout scm
    files = sh(returnStdout: true, script: 'ls')
    println "list of property files"
    p_files = files.split("\n").collect()[2,3]

    sh 'ls | grep prop >> file_list'
    sh '''
    fileprop1=$(cat file_list | head -n1 | tail -n1)
    sed "s/.*/'&',/" $fileprop1 > prop_list1
    sed '$ s/,$//' prop_list1 > temp
    echo "if (Files.equals('$fileprop1')) {return[" | cat - temp > prop_list1
    echo "]} else " >> prop_list1
    
    fileprop2=$(cat file_list | head -n2 | tail -n1)
    sed "s/.*/'&',/" $fileprop2 > prop_list2
    sed '$ s/,$//' prop_list2 > temp
    echo "if (Files.equals('property2')) {return[" | cat - temp > prop_list2
    echo "]}" >> prop_list2
    cat prop_list1 > temp
    cat prop_list2 >> temp
    cat temp | tr -s '\r\n' ' ' > prop_list
    ''' 
    sh '''sed "s/.*/'&',/" file_list > temp1'''
    sh '''sed '$ s/,$//' temp1 > file_list'''
    sh '''sed ''1' s/^/return[/\n' file_list > temp1'''
    sh '''echo "]" >> temp1 && mv temp1 file_list'''

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
                    script: sh(returnStdout:true, script: 'cat ./prop_list')
                ]
                ]
            ]
        ])
    ])
    sh 'echo Hello World'

}
