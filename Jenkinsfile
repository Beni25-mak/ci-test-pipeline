pipeline { 
    agent any 
    environment { 
        DEFAULT_RECIPIENTS = 'benimakumbu24@gmail.com,emmanzimba@gmail.com,nzimbabeni@gmail.com'
        VENV_DIR = 'venv' 
    } 
    stages { 
        stage('Checkout') { 
            steps { 
                git branch: 'main', url: 'https://github.com/Beni25-mak/ci-test-pipeline.git' 
         } 
    } 
    stage('Setup') { 
        steps { 
            bat 'python -m venv venv'  // Crée un environnement virtuel 
                // bat '.\\venv\\Scripts\\pip install -r requirements.txt'  // Installe les dépendances 
        }
    } 
    stage('Run Script') { 
        steps { 
            bat '.\\venv\\Scripts\\python app.py'  // Exécute le script Python 
        } 
    } 
    stage('Notify') { 
        steps { 
            script { 
                def result = currentBuild.result ?: 'SUCCESS' 
            emailext subject: "Jenkins Build: ${result}", 
                body: "Build Status: ${result}\nVoir Jenkins: ${env.BUILD_URL}", 
                to: env.DEFAULT_RECIPIENTS 
            } 
        } 
    } 
} 
    post { 
        failure { 
            emailext subject: "Echec du build Jenkins", 
            body: "Echec du pipeline : ${env.BUILD_URL}", 
            // to: 'benimakumbu24@gmail.com' 
            to:env.DEFAULT_RECIPIENTS
        } 
    } 
} 

// ne me deçois pas mon test
// j'ai confiance