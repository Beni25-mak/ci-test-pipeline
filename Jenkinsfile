pipeline { 
agent any 
environment { 
VENV_DIR = 'venv' 
} 
stages { 
stage('Checkout') { 
steps { 
git branch: 'master', url: 'https://github.com/Beni25-mak/ci-test-pipeline.git' 
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
to: 'benimakumbu24@gmail.com' 
} 
} 
} 
} 
post { 
failure { 
emailext subject: "Échec du build Jenkins", 
body: "Échec du pipeline : ${env.BUILD_URL}", 
to: 'benimakumbu24@gmail.com' 
} 
} 
} 