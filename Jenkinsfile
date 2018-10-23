node {
   withEnv(["PATH+MAVEN=${tool 'apache-maven-3.5.3'}bin"]) {
   stage('Preparation') { 
	checkout scm
	
	}
   stage('Build') {
        mvnHome = tool 'apache-maven-3.5.3'
               sh 'mvn -f controllers-unittest/pom.xml clean install'
   }
    stage('Sonar Analysis') {
            withSonarQubeEnv('sonar') {
                sh 'mvn -f controllers-unittest/pom.xml clean package sonar:sonar'
            }
    stage('Artifacts to Nexus') {
     sh 'curl -v --user admin:admin123 --upload-file /var/lib/jenkins/workspace/AH_org_New_Repo10_master-H5TBAXYMKA7NVHQ6BS2L7CCCBUMK4WW2HEIU226PEIPVF7QSCK6Q/controllers-unittest/target/spring-test-mvc-configuration.war http://nexus.app-cloudfoundry.com/repository/New_repo/'

   }
       stage('Deploy to CF') {
                pushToCloudFoundry cloudSpace: 'dev', credentialsId: 'b7c24062-6ea4-4876-89a1-96b3c2b430b2', manifestChoice: [manifestFile: '/var/lib/jenkins/workspace/AH_org_New_Repo10_master-H5TBAXYMKA7NVHQ6BS2L7CCCBUMK4WW2HEIU226PEIPVF7QSCK6Q/manifest.yml'], organization: ('techm_dev'), selfSigned: ('true'), target: 'api.app-cloudfoundry.com'
        
    }
}
}
}
