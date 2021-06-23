node('kube') {

  def G_TEST1 = "us-west-2"
  def G_TEST2 = "hola"
  def G_TEST3 = "${G_TEST1}:yupyup:${G_TEST2}"
  def AWS_ACCOUNT = "1234567890"
  def AWS_REGION = "us-west-2"
  def NAMESPACE = "la-la-la-cluster"
  def K8_CONTEXT = "arn:aws:eks:${AWS_REGION}:${AWS_ACCOUNT}:cluster/${NAMESPACE}"
  
  stage('Say Hello') {
    sh """
      AWSECR=${AWS_ACCOUNT}.dkr.ecr."${AWS_REGION}".amazonaws.com
      echo ECR: \$AWSECR
    """
    echo "${G_TEST1}"
    G_TEST2 = "${G_TEST1}-${G_TEST2}"
    G_TEST3 = "${G_TEST1}.blabla.${G_TEST2}"
  }
  
  stage('Say Hola') {
    echo "${G_TEST2}"
  }
  
  stage('Say Hi') {
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
