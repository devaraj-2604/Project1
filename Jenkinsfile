pipeline
{
    tools{
        maven 'maven3'
    }
    agent any
    stages
    {
        stage("checkout_source_code")
        {
           steps
            {
             git branch: 'main', url: 'https://github.com/devaraj-2604/Project1.git'
            }
        }
        stage("compile_source_code")
        {
           steps
            {
             sh 'mvn compile'
            }
        }
        stage("run_test")
        {
           steps
            {
            sh 'mvn test'
            }
        }
        stage("create_artifact")
        {
           steps
            {
            sh 'mvn package'
            }
        }
         stage("run_securityscan")
        {
           steps
            {
            sh 'trivy fs --scanners vuln,secret,misconfig .'
            }
        }
        stage("copy_the_artifact")
        {
           steps
            {
            sh 'scp /var/lib/jenkins/workspace/pipelineproject3/target/devops.war ubuntu@172.31.4.40:/var/lib/tomcat9/webapps/test.war'
            }
        }
        stage("run_testcases")
        {
           steps
            {
            sh 'curl http://3.109.56.165:8080/test/  | grep -i Devops'
            sh 'curl http://3.109.56.165:8080/test/  | grep -i apply'
            }
        }
         stage("deploy_theartifactprod")
        {
           steps
            {
            sh 'scp /var/lib/jenkins/workspace/pipelineproject3/target/devops.war ubuntu@172.31.4.243:/var/lib/tomcat9/webapps/test.war'
            }
        }
        
    }
}
