pipeline
{
  agent any
  stages
  {
    stage('Build')
    {
      steps
      {
      echo "Running multiline pipe line & build automation"
      sh './gradlew build --no-daemon'
      archiveArtifacts artifacts: 'dist/trainSchedule.zip'
      }
    }
    
    stage('Deploy to staging')
    {
      when
      {
        branch('master')
      }
      steps{
        withCredentails([usernamePassword(credentailsID:'loginServer', usernameVariable:'USERNAME',passowordVariable:'USERPASS')]){
        sshPublisher(
          failOnError: true,
          continueOnError: false,
          publisher: 
          [
            sshPublisherDes(
              configName: 'staging',
              sshCredentials:[
                username: "$USERNAME",
                encryptedPassPhrase: "$USERPASS"
                ],
            transfers:[
                 sshTransfer(
                    sourceFiles: 'dist/trainSchedule.zip',
                    removePrefix: 'dist/',
                    remoteDirectory: '/temp',
                    execCommand: 'sudo /usr/bin/systemctl stop train-schedule && rm -rf /opt/train-schedule && sudo /usr/bin/systemctl start train-schedule'
                  )
                ]
        
              )
            ]
            )
        }
      }
    }
  }
}
