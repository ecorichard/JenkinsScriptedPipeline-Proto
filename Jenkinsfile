node('kube') {

  def G_TEST1 = "hello"
  def G_TEST2 = "hola"
  def G_TEST3 = ""
  
  stage('Say Hello') {
    echo "${G_TEST1}"
    G_TEST2 = "${G_TEST1}-${G_TEST2}"
    G_TEST3 = "${G_TEST1}.blabla.${G_TEST2}"
  }
  
  stage('Say Hola') {
    echo "${G_TEST2}"
  }
  
  stage('Say Hi') {
    sh """
      localTEST="${G_TEST3}.blabla.${G_TEST2}"
      echo double-quotes: "${G_TEST2}"
      echo double-quotes-merge: "${G_TEST1} -- ${G_TEST2}"
      echo no-quotes: $G_TEST1 -- $G_TEST2
      echo no-quotes-wcurly: ${G_TEST1} -- ${G_TEST2}
      echo G_TEST3: "${G_TEST3}:blabla/${G_TEST2}"
      echo localTEST: $localTEST
    """
  }
  
}
