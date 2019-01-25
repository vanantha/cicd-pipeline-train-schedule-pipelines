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
      sh './gradelw build --no-demon'
      archiveArtifacts artifacts: 'dist/trainSchedule.zip'
      }
    }
  }
}
