pipeline {
 agent any
 tools {
  jdk 'JDK17'
 }
 stages {

  stage('Compile Java') {
   steps {
    sh '''
     rm -rf build
     mkdir build
     javac -d build src/Hello.java
     jar cfe hello.jar Hello -C build .
    '''
   }
  }

  stage('Prepare Package') {
   steps {
    sh '''
     mkdir -p package/usr/local/bin
     cp hello.jar package/usr/local/bin/
    '''
   }
  }

  stage('Build DEB') {
 steps {
  sh '''
   rm -f *.deb
   fpm -s dir -t deb -n hello-java -v 1.0 -C package usr
  '''
 }
}

 }

 post {
  success {
   archiveArtifacts artifacts: '*.deb'
  }
 }
}
