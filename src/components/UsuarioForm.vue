<template>
    <div>


   <Mensagem :msg="msg" v-show="msg"/>



        <form id="usuario-form" @submit="createUser">

            <div class="input-container">

                <label for="nome">Nome do Usuario</label>
                <input type="text" id="nome" v-model="nome" placeholder="Informe  o seu nome">

            </div>



            <div class="input-container">

                <label for="sobrenome">Sobrenome</label>
                <input type="text" id="sobrenome" v-model="sobrenome" placeholder="Informe  o seu nome Sobrenome">

            </div>




            <div class="input-container">

                <label for="email">Email</label>
                <input type="text" id="email" v-model="email" placeholder="Informe o seu email">

            </div>



            <div class="input-container">

                <label for="hora">Horario de Entrada</label>
                <input type="text" id="hora" v-model="entrada" placeholder="Horario de entrada">

            </div>




            <div class="input-container">


                <input type="submit" class="submit-btn" value="Cadastrar Usuario">

            </div>




        </form>

    </div>
</template>


<script>


import Mensagem from './Mensagem.vue';



export default {
    name: "UsuarioForm",


    data(){
        return{
            nome:null,
            sobrenome:null,
            email:null,
            entrada:null,
            msg:null
        }
    },



methods:{


     async createUser(e){
        e.preventDefault();


        const data={
            nome:this.nome,
            sobrenome:this.sobrenome,
            email:this.email,
            entrada:this.entrada,
            msg:"cadastrou",

        }

        // console.log(data);

        const  dataS  = JSON.stringify(data);


        const req = await fetch(" http://localhost:3000/usuarios",{
            method :"POST",
            headers:{"Content-Type" : "application/json"},
            body:dataS
        });

        const res = await req.json();

        console.log(res);


        //Mensagem de  cadastro de carro
        this.msg =`Usuario  ${this.nome} Cadastrado com Sucesso `


        //limpar a mensagem apos um tempo

        setTimeout(()=> this.msg="",2000)
        
        
        
        
        //limpar forms

        this.nome="";
        this.sobrenome="";
        this.email="";
        this.entrada="";
     }
},

components:{
    Mensagem
}


}


</script>


<style scoped>

#usuario-form{

   
    max-width: 300px;
    margin: 0 auto;

}

label{
    font-weight: bold;
    margin-bottom: 15px;
    padding: 5px 10px;
    border-left: 4px solid #000;
}


input{
    padding: 5px 10px;
    widows:300px
}




.input-container{
          display: flex;
          flex-direction: column;
          margin-bottom: 20px;         
}


.submit-btn{
    border-radius: 5px;
    background-color: aqua;
    font-weight: bold;
    transition: .5s;
    cursor: pointer;
}

.submit-btn:hover{
 background-color: violet;
 font-size: 18px;
}


</style>