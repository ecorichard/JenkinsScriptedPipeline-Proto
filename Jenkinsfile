node('kube') {

  def G_TEST1 = "hello"
  def G_TEST2 = "hola"
  
  stage('Say Hello') {
    echo "${G_TEST1}"
    G_TEST2 = "${G_TEST1}-${G_TEST2}"
  }
  
  stage('Say Hola') {
    echo "${G_TEST2}"
  }
  
  stage('Say Hi') {
    sh """
      echo double-quotes: "${G_TEST2}"
      echo double-quotes-merge: "${G_TEST1} -- ${G_TEST2}"
      echo no-quotes: $G_TEST1 -- $G_TEST2
      echo no-quotes-wcurly: ${G_TEST1} -- ${G_TEST2}
    """
  }
  
}
