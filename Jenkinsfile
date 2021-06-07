pipeline {
  agent any
  parameters {
     choice(    name: 'STAGE',
                choices: ['integracion', 'release'],
                description: 'Cual es su accion o destino?'                
              )
    string(name: 'VERSION',
      defaultValue: '',
      description: 'Version? por ejemplo 0.0.1-SNAPSHOT si es integracion o 0.0.1 si es release')
    booleanParam(name: 'cuenta_corriente_ms',
      defaultValue: true,
      description: '')
   
  }
  stages {
    stage('Example') {
      steps {
        echo 'Hello World!'
        echo "Trying: ${params.STAGE}"
        echo "We can dance: ${params.VERSION}"
        echo "The DJ says: ${params.cuenta_corriente_ms}"
      }
    }
  }
}
