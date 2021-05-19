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
          <th>Excluir</th>
        </tr>
      </thead>
      <tbody v-for="(pessoa, index) in pessoas" :key="index">
        <tr>
          <td>{{pessoa.nomeCompleto}}</td>
          <td>{{pessoa.email}}</td>
          <td>{{pessoa.telefone}}</td>
          <td>{{pessoa.cpf}}</td>
          <td>{{pessoa.cnpj}}</td>
          <td><button class="btn-excluir" @click="excluirPessoa(index)"><strong>X</strong></button></td>
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
    excluirPessoa: () => {}
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


  .btn-excluir{
    background-color: red;
    color: #fff;
    padding: .5rem 1rem;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  .btn-excluir:hover{
    background-color: rgb(173, 16, 16);
  }
</style>
