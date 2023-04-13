<template> 
<div class="icons">
  
    <a href="https://www.instagram.com"><img src="./assets/ig.svg"></a> 
    <a href="https://twitter.com"><img src="./assets/tw.svg"></a>
    <a href="https://www.youtube.com"><img src="./assets/yu.svg"> </a>
  
</div>  
  <div class="toggle">
   <span class="sp">Español</span><img src="./assets/toggle.svg" class="iconToggle"><span class="en">English</span>
  </div>
<body> 
  <div class="container">
    <div>
      <h3 class="titleTop">Aumenta tus ingresos a través de tu contenido</h3>
      
      <button class="btnRegister" button @click="irAlPrimerInput">Regrístrate aquí <img src="./assets/arrow.svg" class="arrow"></button>
      
    </div>
    <form class="form" ref="formularioRef" >
      <label for="email"></label>
        <img class="emailIcon" src="./assets/email.svg" >
          <input type="email" name="email" id='email' class="input-field"  v-model="email" @input="validateEmail" :class="{'is-invalid': emailError}" placeholder="Correo Electrónico"  required>
            <div v-if="emailError" class="error-message">Por favor, ingresa un correo válido</div>
              <span v-if="emailIsValid"></span>
                <span v-else></span>

      
      <label for="Name"></label>
        <img class="userIcon" src="./assets/user.svg" alt="">
          <input type="text"  name="name" id="name" v-model="name" placeholder="Nombre Completo"  required>
          
      
      <label for="Fecha"></label>
        <img class="calendarIcon" src="./assets/calendar.svg">
          <input type="date" format="yyyy-MM-DD" name="fecha" id="fechaNacimiento" v-model="fecha" placeholder="Fecha de Nacimiento"  required>
            <span v-if="fechaIsValid"></span>
              <span v-else></span>
      
      <label for="Contraseña"></label>  
        <img class="lockIcon" src="./assets/lock.svg" alt="">
          <input type="password" name="password" id="password" v-model="password" placeholder="Contraseña" required>
       
      <label for="Repetircontraseña"></label> 
        <img class="lockIcon1" src="./assets/lock.svg" alt="">
          <input type="password"  name="password" id="Rpassword" v-model="Rpassword" placeholder="Repetir Contraseña" required>
    </form>
      <h4 class="titleBottom">Al completar el registro, usted está aceptando nuestras <span class="bold-text">políticas de privacidad</span>  y <span class="bold-text">términos de servicio</span>, además confirma que cumple con la mayoria de edad de su lugar de residencia</h4>
      
      <div v-for="(paso, index) in pasos" :key="index" v-show="index === pasoActual">
           <component :is="paso.componente" @validado="onValidado" />
      </div>

      <div @submit.prevent="submitForm">
          <button @click="showModal = true">Registrarse</button>
        </div> 

        <div classs="modal" v-if="showModal">
          <div class="modal-content">¡Formulario enviado con éxito!</div>
            
        </div>  
      <div>
        <span v-for="(paso, index) in pasos" :key="index">
         {{ paso.email }} {{ index === pasos.length - 1 ? '' : ' ' }}
        </span>
      </div>
  </div>
</body>
</template>

<script>


 export default {
   data() {
     return {
      email: '',  
      name: '', 
      fecha: '',
      password: '',
      Rpassword: '',
      languageActive: false,
      pasoActual: 0,
      pasoActualValido: false,
      pasos: [
         { nombre: '', componente: 'Paso1', camposObligatorios: ['email'] },
         { nombre: '', componente: 'Paso2', camposObligatorios: ['name', 'fecha', 'password', 'Rpassword'] },
       ],
      
    }
  }, 
  methods: { 
    validateEmail() {
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

      if (!emailRegex.test(this.email)) {
        this.emailError = true;
      } else {
        this.emailError = false;
      }
    },
      
  },
    submitForm() {
        this.showConfirmation = true;
        this.showModal = false;
      },
      irAlPrimerInput() {
      this.$refs.formularioRef.querySelector('input').focus();
    },
   

   
    computed: {  
      emailIsValid() {
        return this.email.includes('@') && this.email.includes('.')
      },

      fechaIsValid(){
        const regex = /^\d{2}\/\d{2}\/\d{4}$/;
        return regex.test(this.fecha);
      }, 
    }
   }   
</script>
<style>
@import '@fortawesome/fontawesome-free/css/all.css';

*{
  font-family: 'Poppins';
  font-size: 16px;
  
}

body{
  background-image: url("./assets/Fondo.jpg");
  background-repeat: no-repeat ;
  background-size: cover;

}

.icons{
  padding: 5px;
  
}


.toggle{
  margin: auto 0;
  text-align: right;
  position: relative;
  bottom: 30px ;
}

.iconToggle{
  padding: 5px;
  width: 30px;
}

.sp{ 
  position: relative;
  bottom: 13px;
}

.en{ 
  position: relative;
  bottom: 13px;
}

.titleTop{
  display: flex;
  margin: 0 auto;
  padding: 15px;
  text-align: center;
  font-size: 16px;
  color: #AFAFAF;
  width: 18%;
}

.titleBottom{
  display: flex;
  margin: 0 auto;
  padding: 15px;
  text-align: center;
  font-size: 12px;
  color: #AFAFAF;
  width: 30%;
}

.arrow{
  position: relative;
  left: 100px;
  bottom: 30px;

}

.bold-text{
  padding: 3px;
  display: flex;
  margin: 0 auto;
  font-size: 12px;
  font-weight: bold;
  color: #000000;
}

label{ 
  display: flex;
  padding: 15px;  
}

.emailIcon{
  width: 20px;
  margin: 0 auto;
  display: flex;
  position: relative;
  right: 200px;
  top: 35px;
  fill: #ffffff;
}

.userIcon{
  width: 20px;
  margin: 0 auto;
  display: flex;
  position: relative;
  right: 200px;
  top: 35px;
}

.lockIcon{
  width: 20px;
  margin: 0 auto;
  display: flex;
  position: relative;
  right: 200px;
  top: 35px;
}

.lockIcon1{ 
  width: 20px;
  margin: 0 auto;
  display: flex;
  position: relative;
  right: 200px;
  top: 35px;
}

.calendarIcon{
  width: 20px;
  margin: 0 auto;
  display: flex;
  position: relative;
  right: 200px;
  top: 35px;

}


input[type="email"], 
input[type="text"],
input[type="date"],
input[type="password"]{
  border: none;
  display: flex;
  margin: 0 auto;
  border-radius: 8px;
  color: #616060;
  padding-left: 40px;
  width: 400px;
  height: 50px;
 
}

.placeholder{
  font-weight: bolder;
}

button{
  padding: 15px;
  text-align: center;
  display: block;
  margin: 0 auto;
  background-color: #5F3C84;
  color: #ffff;
  padding: 10px 45px;
  border: none;
  border-radius: 20px;
  cursor: pointer;
  width: 450px;
  box-shadow: 0 8px 24px 0 rgba(219, 101, 243, 0.2);
}

.btnRegister{
  
  width: 250px;
  height: 40px;
  font-weight: 500;
  box-shadow: 0 8px 24px 0 rgba(219, 101, 243, 0.2);
  
  

}

.btnRegister::after{
  content: "";
  position: absolute;
  right: 20px ;
}

button:active,
button:focus{  
  background-color: #2C1C3D;
  color: #ffffff;
  box-shadow: 0 8px 24px 0 rgba(16,39,112,.2);
}
button:hover{  
  background-color: #2C1C3D;
  color: #ffffff;
  box-shadow: 0 8px 24px 0 rgba(16,39,112,.2);
}

.arrow{
  fill: #ffff;
  width: 30px;
  
}



</style>


