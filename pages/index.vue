<template>
  <section class="container mt-5">
    <h2 class='mb-4 text-center'>連絡先リスト</h2>
    <table class="table">
      <thead>
        <tr>
          <th>ID</th>
          <th>名前</th>
          <th>住所</th>
          <th>電話番号</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for='contact in contacts' :key='contact.id'>
          <td>{{contact.id}}</td>
          <td>{{contact.name}}</td>
          <td>{{contact.address}}</td>
          <td>{{contact.tel}}</td>
          <td>
            <a href="#" class="btn btn-success btn-sm">編集</a>
            <a href="#" class="btn btn-danger btn-sm">削除</a>
          </td>
        </tr>
      </tbody>
    </table>
    <b-btn variant="primary" @click="newContact">新規登録</b-btn>

    <b-modal v-model="showModal" id="contactModal" :title="modalTitle">
      <b-form>
        <b-form-group label="名前" label-for="name">
          <b-form-input type="text" v-model="modalContact.name" :state="!$v.modalContact.name.$invalid" aria-describedby="nameFeedback"></b-form-input>
          <b-form-invalid-feedback id="nameFeedback">名前は 2-10 文字で入力してください</b-form-invalid-feedback>
        </b-form-group>
        <b-form-group label="住所" label-for="address">
          <b-form-input type="text" v-model="modalContact.address" :state="!$v.modalContact.address.$invalid" aria-describedby="addressFeedback"></b-form-input>
          <b-form-invalid-feedback id="addressFeedback">住所は 10-20 文字で入力してください</b-form-invalid-feedback>
        </b-form-group>
        <b-form-group label="電話番号" label-for="tel">
          <b-form-input type="text" v-model="modalContact.tel" :state="!$v.modalContact.tel.$invalid" aria-describedby="telFeedback" ></b-form-input>
          <b-form-invalid-feedback id="telFeedback">電話番号は 10-13 文字で入力してください</b-form-invalid-feedback>
        </b-form-group>
      </b-form>

      <div slot="modal-footer" class="w-100">
        <div class="float-right">
          <b-btn size="sm" variant="default" @click="showModal = false">
            キャンセル
          </b-btn>
          <b-btn size="sm" class="ml-1" :variant="modalButtonClass" @click="saveContact" :disabled="$v.modalContact.$invalid">
            {{modalButtonText}}
          </b-btn>
        </div>
      </div>
    </b-modal>
  </section>
</template>

<script>
import Vue from 'vue'
import { validationMixin } from "vuelidate"
import { required, minLength, maxLength } from "vuelidate/lib/validators"

export default {
  data () {
    return {
      modalContact: {},
      showModal: false,
      contacts: [
        { id: 1, name: '山田太郎', address: '東京都渋谷区', tel: '09012340001' },
        { id: 2, name: '田中陽子', address: '北海道札幌市', tel: '09012340002' },
        { id: 3, name: '佐藤一郎', address: '沖縄県那覇市', tel: '09012340003' },
      ],
    }
  },
  mixins: [
    validationMixin
  ],
  computed: {
    idExists () {
      return this.modalContact && this.modalContact.id
    },
    modalTitle () {
      return this.idExists ? '連絡先編集' : '連絡先新規登録'
    },
    modalButtonClass () {
      return this.idExists ? 'success' : 'primary'
    },
    modalButtonText () {
      return this.idExists ? '更新する' : '登録する'
    },
  },
  validations: {
    modalContact: {
      name: {
        required,
        minLength: minLength(2),
        maxLength: maxLength(10)
      },
      address: {
        required,
        minLength: minLength(10),
        maxLength: maxLength(20)
      },
      tel: {
        required,
        minLength: minLength(10),
        maxLength: maxLength(13)
      },
    }
  },
  methods: {
    newContact () {
      this.modalContact = {}
      this.showModal = true
    },
    saveContact () {

    }
  }
}
</script>
