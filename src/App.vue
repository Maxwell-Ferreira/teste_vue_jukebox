<template>
  <div class="form">
    <h1 v-if="!editar">Cadastro de pessoa</h1>
    <h1 v-else>Editar pessoa</h1>
    <form action="">
      <div class="form-group">
        <label for="">Nome</label><br/>
        <input type="text" id="nome" v-model="pessoa.nome">
      </div>
      <div class="form-group">
        <label for="">Sobrenome</label><br/>
        <input type="text" id="sobrenome"  v-model="pessoa.sobrenome">
      </div>
      <div class="form-group">
        <label for="">Email</label><br/>
        <input type="email" id="email" v-model="pessoa.email">
      </div>
      <div class="form-group">
        <label for="">Telefone</label><br/>
        <input type="text" id="telefone" v-model="pessoa.telefone">
      </div>
      <div class="form-group">
        <label for="" style="margin-right: 6px">Pessoa Juridica?</label>
        <input type="checkbox" id="pessoaJuridica" v-model="pessoaJuridica">
      </div>
      <div v-if="!pessoa.pessoaJuridicaTrigger" class="form-group">
        <label for="">CPF</label><br/>
        <input type="text" id="cpf" v-model="pessoa.cpf">
      </div>
      <div v-else class="form-group">
        <label for="">CNPJ</label><br/>
        <input type="text" id="cnpj" v-model="pessoa.cnpj">
      </div>
      <div v-if="!editar" class="form-group">
        <button @click="cadastrarPessoa">Cadastrar pessoa</button>
      </div>
      <div v-else class="form-group">
        <button @click="salvarPessoa">Salvar pessoa</button>
      </div>
    </form>
  </div>
  <Tabela 
    :pessoas="pessoas" 
    :excluirPessoa="(index) => excluirPessoa(index)"
    :editarPessoa="(index) => editarPessoa(index)"
  />
</template>

<script>
import Tabela from "./components/Tabela.vue";

export default {
  name: "App",
  components: {
    Tabela,
  },
  data(){
    return {
      editar: false,
      pessoaEditada: 0,
      pessoas: [],
      pessoa:{
        nome: "",
        sobrenome: "",
        email: "",
        telefone: "",
        pessoaJuridicaTrigger: false,
        cpf: "",
        cnpj: ""
      },
      pessoaJuridica: false
    }
  },
  watch: {
    pessoaJuridica(){
      if(this.pessoa.pessoaJuridicaTrigger){
        this.pessoa.cpf = "";
      }else{
        this.pessoa.cnpj = "";
      }
      this.pessoa.pessoaJuridicaTrigger = !this.pessoa.pessoaJuridicaTrigger;
    }
  },
  computed: {
    nomeCompleto(){
      return `${this.pessoa.nome} ${this.pessoa.sobrenome}`;
    }
  },
  methods: {
    cadastrarPessoa(e){
      e.preventDefault();

      let novaPessoa = {
        nomeCompleto: this.nomeCompleto,
        ...this.pessoa
      }

      this.pessoas.push(novaPessoa);
      
      let persistPessoaJuridica = this.pessoaJuridica;
      this.pessoa = {
        nome: "",
        sobrenome: "",
        email: "",
        telefone: "",
        pessoaJuridica: false,
        pessoaJuridicaTrigger: persistPessoaJuridica,
        cpf: "",
        cnpj: ""
      }
    },

    excluirPessoa(index){
      this.pessoas.splice(index, 1);
    },

    salvarPessoa(e){
      e.preventDefault();

      let novosDados = {
        nomeCompleto: this.nomeCompleto,
        ...this.pessoa
      }

      if(novosDados.pessoaJuridicaTrigger){
        novosDados.cpf = "";
      }else{
        novosDados.cnpj = "";
      }

      this.pessoas[this.pessoaEditada] = novosDados;

      let persistPessoaJuridica = this.pessoaJuridica;
      this.pessoa = {
        nome: "",
        sobrenome: "",
        email: "",
        telefone: "",
        pessoaJuridica: false,
        pessoaJuridicaTrigger: persistPessoaJuridica,
        cpf: "",
        cnpj: ""
      }

      this.editar = false;
    },

    editarPessoa(index){
      var dados = {...this.pessoas[index]};
      delete dados.nomeCompleto;
      this.pessoa = dados;
      
      this.pessoaEditada = index;
      this.editar = !this.editar;
    }
  }
};
</script>

<style>

body{
  background-color: rgb(245, 255, 245);
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px;
  display: flex;
  
  align-items: flex-start;
  justify-content: space-between;
}

.form{
  width: 20vw;
  padding: 30px;
  height: 70vh;
  background-color: rgb(210, 236, 202);
  border-radius: 4px;
  display: flex;
  flex-direction: column;
  align-content: center;
  justify-content: center;
}

form {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.form-group{
  padding: .6rem;
  text-align: left;
  width: 100%;
}

input{
    padding: .4rem;
    border: 1px solid rgb(206, 206, 206);
    border-radius: 4px;
    width: calc(100% - 30px);
}

button{
  background-color: rgb(58, 64, 151);
  color: #fff;
  padding: .5rem 1rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover{
  background-color: rgb(41, 45, 105);
}


</style>
