---
title: Variables, Loops, Conditionals in Ansible
nav: true
---

# Variables, Loops, Conditionals in Ansible

## Variables
Variable in playbooks are similar to variables in any programming language. 
It helps you to use and assign a value to a variable and use that anywhere in the playbook. 
One can put conditions around the value of the variables and accordingly use them in the playbook

### Example 1
    
        - hosts : <your hosts> 
        vars:
        tomcat_port : 8080 

In the above example, we have defined a variable name tomcat_port and assigned the value 8080 to that variable and can use that in your playbook wherever needed.

### Example 2

      block: 
      - name: Install Tomcat artifacts 
          action: > 
          yum name = "demo-tomcat-1" state = present 
          register: Output 
          
      always: 
        - debug: 
           msg: 
              - "Install Tomcat artifacts task ended with message: {{Output}}" 
              - "Installed Tomcat artifacts - {{Output.changed}}" 

Here, output is the variable used.

Let us walk through all the keywords used in the above code −

block − Ansible syntax to execute a given block.

name − Relevant name of the block - this is used in logging and helps in debugging that which all blocks were successfully executed.

action − The code next to action tag is the task to be executed. The action again is a Ansible keyword used in yaml.

register − The output of the action is registered using the register keyword and Output is the variable name which holds the action output.

always − Again a Ansible keyword , it states that below will always be executed.

msg − Displays the message.

The expression {{Output}}  will read the value of variable Output. Also as it is used in the msg tab, it will print the value of the output variable.


## Loops

Below is the example to demonstrate the usage of Loops in Ansible.
The tasks is to copy the set of all the war files from one directory to tomcat webapps folder.
Here, we will concentrate on the usage of loops.
Initially in the 'shell' command we have done ls *.war. So, it will list all the war files in the directory.
Output of that command is taken in a variable named output.
To loop, the 'with_items' syntax is being used.
with_items: "{{output.stdout_lines}}" --> output.stdout_lines gives us the line by line output and then we loop on the output with the with_items command of Ansible.
Attaching the example output just to make one understand how we used the stdout_lines in the with_items command.

    #Testing 
    - hosts: tomcat-node 
       tasks: 
          - name: Install Apache 
          shell: "ls *.war" 
          register: output 
          args: 
             chdir: /opt/ansible/tomcat/demo/webapps 

          - file: 
             src: '/opt/ansible/tomcat/demo/webapps/{{ item }}' 
             dest: '/users/demo/tom/{{ item }}' 
             state: link 
          with_items: "{{output.stdout_lines}}"
          
## Conditionals
Conditionals are used where one needs to run a specific step based on a condition.

    #Testing 
    - hosts: all 
       vars: 
          test1: "Hello Tom" 
       tasks: 
          - name: Testing Ansible variable 
          debug: 
             msg: "Equals" 
             when: test1 == "Hello Tom" 
             
In this case, Equals will be printed as the test1 variable is equal as mentioned in the when condition. 
'when' can be used with a logical OR and logical AND condition as in other the programming languages.

  

