# validador-angular-cedula-ecuador
Validación de cédula en Angular JS

En el component.html se puede crear un input para verificar la cédula mientras va escribiendola mediante (change) el cual llama al método validadorDeCedula en el component.ts y mediante una variable "validador" se presentara el mensaje de validación o no.

     <input type="text" value="" name="cedula" [(ngModel)]="cedula" (change)="validadorDeCedula(cedula)" maxlength="10">
                 <small *ngIf="!validador" class="text-danger">Cedula Invalida</small>

EL método de validación del component.ts es el siguiente:

    //esta es la variable de validación
    public validador; 
    validadorDeCedula(cedula: String) {
      let cedulaCorrecta = false;
      if (cedula.length == 10)
      {    
          let tercerDigito = parseInt(cedula.substring(2, 3));
          if (tercerDigito < 6) {
              // El ultimo digito se lo considera dígito verificador
              let coefValCedula = [2, 1, 2, 1, 2, 1, 2, 1, 2];       
              let verificador = parseInt(cedula.substring(9, 10));
              let suma:number = 0;
              let digito:number = 0;
              for (let i = 0; i < (ced
              ula.length - 1); i++) {
                  digito = parseInt(cedula.substring(i, i + 1)) * coefValCedula[i];      
                  suma += ((parseInt((digito % 10)+'') + (parseInt((digito / 10)+''))));
            //      console.log(suma+" suma"+coefValCedula[i]); 
              }
              suma= Math.round(suma);
            //  console.log(verificador);
            //  console.log(suma);
            //  console.log(digito);
              if ((Math.round(suma % 10) == 0) && (Math.round(suma % 10)== verificador)) {
                  cedulaCorrecta = true;
              } else if ((10 - (Math.round(suma % 10))) == verificador) {
                  cedulaCorrecta = true;
              } else {
                  cedulaCorrecta = false;
              }
          } else {
              cedulaCorrecta = false;
          }
      } else {
          cedulaCorrecta = false;
      }
    this.validador= cedulaCorrecta;

    }
