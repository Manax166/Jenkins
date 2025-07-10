pipeline {
    agent any
    environment {
        value = "blabla"
    }
    stages {
        stage("etape 1") {
            steps {
                echo "cette première pipeline est fonctionnelle" 
                script {
                    def newValue = 42
                    echo "${newValue}"
                }
            }
        }
        stage("etape 2") {
            steps {
                echo "Voici mon incroyable valeur secrète : ${value} !"
            }
        }
        stage("operations") {
            steps {
                script {
                    for (def variableBoucle = 0; variableBoucle < 3; variableBoucle++) {
                        echo "boucle for classique : ${variableBoucle}"
                    }
                    for (variableBoucle in 1..3) {
                        echo "boucle for in : ${variableBoucle}"
                    }
                    /*while (cpt<3) {
                        //echo "boucle while : ${cpt}"
                        //cpt++
                    }*/
                    def items = ["pomme", "poire", "banane"]
                    items.each { item ->
                        echo "${item}"
                    }
                }
            }
        }
        stage("approbation") {
            steps {
                input message: "continuer", ok: "Oui", cancel: "Non"
            }
        }
        
        stage("parallel test") {
            parallel {
                stage("tryCatch") {
                    steps {
                        script {
                            try {
                                def reponse = httpRequest 'https://httpbin.org/get'
                                println reponse.content
                            } catch (Exception e) {
                                error "erreur : ${e.message}"
                            }
                        }
                    }
                }
                stage("meanwhile") {
                    steps {
                        echo "test"
                        sleep 5
                        echo 'fin de meanwhile'
                    }
                }
                stage("meanwhile2") {
                    steps {
                        script {
                            def calc = 14+62000
                            echo "${calc}"
                        }
                    }
                }
            }
        }
    }
    post {
        success {
            echo "ça marche :)"
        }
        failure {
            echo "ça ne marche pas :("
        }
        always {
            echo "ça fait toujours ce message à la fin"
        }
    }
}
