node('kube') {
  initEnvVars()

  def G_TEST1 = "us-west-2"
  def G_TEST2 = "hola"
  def G_TEST3 = "${G_TEST1}:yupyup:${G_TEST2}"
  def AWS_ACCOUNT = "1234567890"
  def AWS_REGION = "us-west-2"
  def NAMESPACE = "la-la-la-cluster"
  def K8_CONTEXT = "arn:aws:eks:${AWS_REGION}:${AWS_ACCOUNT}:cluster/${NAMESPACE}"
  
  stage('Say Hello') {
    sh '''
      printenv | sort
    '''
    sh """
      AWSECR=${AWS_ACCOUNT}.dkr.ecr.${AWS_REGION}.amazonaws.com
      echo ECR: \$AWSECR
    """
    echo "${G_TEST1}"
    G_TEST2 = "${G_TEST1}-${G_TEST2}"
    G_TEST3 = "${G_TEST1}.blabla.${G_TEST2}"
    env.setProperty('ENV_VERSION', '007')
  }
  
  stage('Say Hola') {
    echo "${G_TEST2}"
    stashEnvVars()
  }
}

node('kube') {
  initEnvVars()
  
  stage('print env 2') {
    sh '''
      printenv | sort
    '''
  }
  stage('test load stash') {
    loadStashToEnv()
  }
  stage('Say Hi') {
    sh '''
      echo "----test load------"
      printenv | grep 'ENV_' | sort
    '''
    sh """
      localTEST=${G_TEST3}.blabla.${G_TEST2}.test.com
      echo double-quotes: "${G_TEST2}"
      echo double-quotes-merge: "${G_TEST1} -- ${G_TEST2}"
      echo no-quotes: $G_TEST1 -- $G_TEST2
      echo no-quotes-wcurly: ${G_TEST1} -- ${G_TEST2}
      echo G_TEST3: "${G_TEST3}:blabla/${G_TEST2}"
      echo "localTEST: \$localTEST"
    """
  }
  
}

def stashEnvVars() {
  sh '''
    echo "ENV_AWS_ACCOUNT=$ENV_AWS_ACCOUNT" > envVars.txt
    echo "ENV_AWS_REGION=$ENV_AWS_REGION" >> envVars.txt
    echo "ENV_NAME=$ENV_NAME" >> envVars.txt
    echo "ENV_VERSION=$ENV_VERSION" >> envVars.txt
    echo "ENV_NAMESPACE=$ENV_NAMESPACE" >> envVars.txt
    echo "ENV_CONFIG=$ENV_CONFIG" >> envVars.txt
  '''
  stash name: 'envVars', includes: 'envVars.txt'
}

def initEnvVars() {
  env.setProperty('ENV_AWS_ACCOUNT', '1234567890')
  env.setProperty('ENV_AWS_REGION', 'us-west-2')
  env.setProperty('ENV_NAME', 'xyz-abc-job')
  env.setProperty('ENV_VERSION', '')
  env.setProperty('ENV_NAMESPACE', 'hello-cluster-world')
  env.setProperty('ENV_CONFIG', 'hello-you')
}

def loadStashToEnv() {
  unstash :	'envVars'
  sh '''
     export $(cat envVars.txt)
     printenv | grep 'ENV_' | sort
  '''
  sh '''
    printenv | grep 'ENV_' | sort
  '''
}  
