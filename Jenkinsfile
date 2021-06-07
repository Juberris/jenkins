  // proyectos front end
  def ui = ['sag-ui']; 
  // proyectos backend (nombres de directorios)
 
  def ms_cta_cte = ['cuenta-corriente-ms'];
  def ms_bitacora = ['sag-bitacora-ms']; 
  def ms_emision = ['sag-emisiongiro-ms'];
  def ms_giros = ['sag-giros-ms']; 
  def ms_mantenedores = ['sag-mantenedores-ms']; 
  def ms_notificacion = ['sag-notificacion-ms'];
  def ms_solicitudes = ['sag-solicitudes-ms'];
  def ms=[];

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
     choice(    name: 'REST',
                choices: ['','sag-giros-ms','cuenta-corriente-ms','sag-bitacora-ms','sag-emisiongiro-ms','sag-solicitudes-ms','sag-notificacion-ms','sag-pagos-ms'],
                description: 'Seleccione microservicio'                
              )    
     booleanParam(name: 'sag_ui',
      defaultValue: true,
      description: '')
  }
  stages {
    
     stage ('Validate Version') {
      steps {
        script {
          // tenemos que validar que la version sea valida y del formato requerido
          def current_tag = params.VERSION
          def snapshot = current_tag.endsWith("-SNAPSHOT")
          if(!current_tag || current_tag == '' || (params.STAGE == 'integracion' && !snapshot) || (params.STAGE == 'release' && snapshot)){
              error "Se requiere setear version y debe estar en formato X.Y.Z-SNAPSHOT si es integracion o X.Y.Z si es release: ${params.VERSION}" 
          } else{
            def major = (current_tag =~ /\d+\.\d+\.\d+[-]?(alpha|rc)?(\d)?{1,2}/)
            if (major) { 
              // significa que cumple con la regla de tag en nombrado y es deployable.
              println major.group()
            } else {
              error "Tag sin formato valido : ${params.VERSION} " 
            }              
          }
        }
      }
    }
    
     stage('Build Backend') {
     
      steps {
        script {
          if( params.RESTSERVICE != ''){
              ms=[params.RESTSERVICE]
              ms.each {
                dir(path: "backend/${it}") {
                  echo "${it}"
                }  // end dir
              } // end for
          }else{
            error "Debe seleccionar un microservicio!"
          }
        }
      } // end step
    } // end stage 
    
  }
}
