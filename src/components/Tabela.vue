<template>
  <div class="tabela">
    <h1> Pessoas Cadastradas</h1>
    <table>
      <thead>
        <tr>
          <th>Nome Completo</th>
          <th>Email</th>
          <th>Telefone</th>
          <th>CPF</th>
          <th>CNPJ</th>
          <th>Ações</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(pessoa, index) in pessoas" :key="index">
          <td>{{pessoa.nomeCompleto}}</td>
          <td>{{pessoa.email}}</td>
          <td>{{pessoa.telefone}}</td>
          <td>{{pessoa.cpf}}</td>
          <td>{{pessoa.cnpj}}</td>
          <td>
            <button class="btn btn-excluir" @click="excluirPessoa(index)"><strong>X</strong></button>
            <button class="btn btn-editar" @click="editarPessoa(index)"><strong>E</strong></button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "Tabela",
  props: {
    pessoas: [],
    excluirPessoa: () => {},
    editarPessoa: () => {}
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .tabela{
    background-color: rgb(210, 236, 202);
    padding: 30px;
    width: 55vw;
    height: 70vh;
    border-radius: 4px;
    display: flex;
    flex-direction: column;
    align-items: center;
    overflow-y: auto;
  }

  table{
    border-spacing: 0;
    width: 100%;
  }

  th{
    padding: .7rem;
    background-color: rgb(172, 221, 196);
    color: #000;
    border: 1px solid rgb(185, 185, 185);
  }

  td{
    margin: 0;
    padding: .6rem;
    background-color: #fff;
    border: 1px solid rgb(185, 185, 185);
    border-spacing: 0;
    animation: tdAnimation 1s;
    overflow: hidden;
  }

  .btn{
    margin: 0 5px;
    padding: .5rem 1rem;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  .btn-excluir{
    background-color: rgb(255, 75, 75);
    color: #fff;
    
  }
  .btn-excluir:hover{
    background-color: rgb(228, 40, 40);
  }

  .btn-editar{
    background-color: rgb(255, 231, 93);
    color: #000;
  }

  .btn-editar:hover{
    background-color: rgb(224, 203, 80);
    color: #000;
  }

  @keyframes tdAnimation {
    0% {
      transform: translateY(-1.2rem);
    }
    40% {
      transform: translateY(-1.2rem);
    }
    100% {
      transform: translateY(0);
    }
  }

</style>
