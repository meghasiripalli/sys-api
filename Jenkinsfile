pipeline {
  agent any
  tools {
    maven 'Maven'
    jdk 'JDK 8'
  }
  stages {
    stage('Build') {
      steps {
        withEnv(overrides: ["JAVA_HOME=${ tool 'JDK 8' }", "PATH+MAVEN=${tool 'Maven'}/bin:${env.JAVA_HOME}/bin"]) {
         bat 'mvn -f pom.xml clean install -e -Denv=dev -Dkey=mule -DskipTests'
       }
      }

    }
    
    stage('Unit Test') {
      steps {
        withEnv(overrides: ["JAVA_HOME=${ tool 'JDK 8' }", "PATH+MAVEN=${tool 'Maven'}/bin:${env.JAVA_HOME}/bin"]) {
        bat 'mvn -f pom.xml -Denv=dev -Dkey=mule test'
        }
      }

    }

    stage('Deploy') {
      steps {
        withEnv(overrides: ["JAVA_HOME=${ tool 'JDK 8' }", "PATH+MAVEN=${tool 'Maven'}/bin:${env.JAVA_HOME}/bin"]) {
        bat 'mvn -f pom.xml package deploy -DmuleDeploy -Denv=dev -Dkey=mule -Danypoint.username=njctrail -Danypoint.password=Njc@1234 -DapplicationName=sap-sapi '
        }
      }
    }
  }
}
