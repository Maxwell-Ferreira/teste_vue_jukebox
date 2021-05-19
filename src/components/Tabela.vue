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
      <tbody v-for="(pessoa, index) in pessoas" :key="index">
        <tr>
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

  table{
    border-spacing: 0;
    max-width: 800px;
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
    border: 1px solid rgb(185, 185, 185);
    border-spacing: 0;
  }

  .btn{
    padding: .5rem 1rem;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  .btn-excluir{
    background-color: red;
    color: #fff;
    
  }
  .btn-excluir:hover{
    background-color: rgb(173, 16, 16);
  }

  .btn-editar{
    background-color: rgb(235, 238, 38);
    color: #000;
  }

  .btn-editar:hover{
    background-color: rgb(153, 172, 45);
    color: #000;
  }
</style>
