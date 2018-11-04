<template>
  <section class="container">
    <h2 class='mt-5 mb-5 text-center'>連絡先リスト</h2>
    <table class="table">
      <thead>
        <tr>
          <td>ID</td>
          <td>名前</td>
          <td>住所</td>
          <td>電話番号</td>
          <td></td>
        </tr>
      </thead>
      <tbody>
        <tr v-for='contact in contacts' :key='contact.id'>
          <td>{{contact.id}}</td>
          <td>{{contact.name}}</td>
          <td>{{contact.address}}</td>
          <td>{{contact.tel}}</td>
          <td>
          </td>
        </tr>
      </tbody>
    </table>
  </section>
</template>

<script>
export default {
  data () {
    return {
      contacts: [],
    }
  },
}
</script>
