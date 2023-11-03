<template>
    <div id="usuario-table">
        <Mensagem :msg="msg" v-show="msg" />
        <table class="simple-table">
            <thead>
                <tr>
                    <th>#</th>
                    <th>Nome</th>
                    <th>Sobrenome</th>
                    <th>Email</th>
                    <th>Horário de Entrada</th>
                    <th>Ações</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="usuario in usuarios" :key="usuario.id">
                    <td>{{ usuario.id }}</td>
                    <td>{{ usuario.nome }}</td>
                    <td>{{ usuario.sobrenome }}</td>
                    <td>{{ usuario.email }}</td>
                    <td>{{ usuario.entrada }}</td>
                    <td>
                        <select name="status" class="status " @change="editarUsuario($event, usuario.id)">
                            <option value=""> Status </option>
                            <option :value="statu.tipo" v-for="statu in status" :key="statu.id" :selected="usuario.status == statu.tipo">{{ statu.tipo }} </option>
                            
                            
                        </select>
                        <button class="delete-btn" @click="deletarUsuario(usuario.id)">Deletar</button>
                        
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
  


<script>



import Mensagem from './Mensagem.vue';

export default {

    name: "exibir",

    data() {
        return {
            usuarios: null,
            usuarios_id: null,
            status: [],
            msg: null
        }
    },


    components : {

Mensagem
},

    methods: {

        async getCadastros() {

            const req = await fetch("http://localhost:3000/usuarios");

            const data = await req.json();

            this.usuarios = data;

            this.getStatus();

        },



        async getStatus() {

            const req = await fetch("http://localhost:3000/status");

            const data = await req.json();

            this.status = data;


        },



        async deletarUsuario(id) {


            const req = await fetch(`http://localhost:3000/usuarios/${id}`, {
                method: "DELETE"

            })


            this.msg = `Usuario  DELETADO com sucesso. Obrigado `;
            
            setTimeout(() => this.msg = "", 3000)





            this.getCadastros();

        },




        async editarUsuario(event, id) {


            const opcoes = event.target.value;

            const data = JSON.stringify({ status: opcoes })

            const req = await fetch(`http://localhost:3000/usuarios/${id}`, {


                method: 'PATCH',

                headers: { 'Content-Type': 'application/json', },
                body: data


            });


            const res = await req.json();



                    
                    this.msg = `Usuario : ${res.nome} foi atualizado Com Sucesso . Obrigado `;


              setTimeout(() => this.msg = "", 3000)







          





        }






    },






    mounted() {
        this.getCadastros()
    }

}

</script>


<style>
.simple-table {
    border-collapse: collapse;
    width: 100%;
}

.simple-table th,
.simple-table td {
    border: 1px solid #ccc;
    padding: 8px;
    text-align: left;
}


.status,
.delete-btn {
    padding: 6px 10px;
    border: none;
    background-color: #007BFF;
    color: #fff;
    cursor: pointer;
    margin-right: 5px;
}

.update-btn {
    padding: 6px 10px;
    border: none;
    background-color: rgb(81, 255, 0);
    color: #fff;
    cursor: pointer;
    margin-right: 5px;
}

.status {
    padding: 6px 10px;
    background-color: rgb(104, 143, 86);
    color: #fff;
    cursor: pointer;

}
</style>