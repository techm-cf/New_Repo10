node {
   withEnv(["PATH+MAVEN=${tool 'apache-maven-3.5.3'}bin"]) {
   stage('Preparation') { 
	checkout scm
	
	}
   stage('Build') {
        mvnHome = tool 'apache-maven-3.5.3'
               sh 'mvn -f controllers-unittest/pom.xml clean install'
}
}
}
