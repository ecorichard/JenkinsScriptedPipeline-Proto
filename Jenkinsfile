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
}
