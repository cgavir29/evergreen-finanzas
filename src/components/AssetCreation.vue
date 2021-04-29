<template>
  <section class="mb-6">
    <b-field label="Description">
      <b-input v-model="description" placeholder="Description"></b-input>
    </b-field>

    <b-field label="Value">
      <b-numberinput v-model="value" placeholder="357" min="0"></b-numberinput>
    </b-field>

    <b-field label="Type">
      <b-input v-model="type" placeholder="Type"></b-input>
    </b-field>

    <b-button class="mt-3" type="is-success" @click="createAsset"
      >Create</b-button
    >
  </section>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      description: '',
      value: null,
      type: '',
    };
  },
  methods: {
    createAsset() {
      if (this.description != '' && this.value != null && this.type != '') {
        axios
          .post(
            'https://be.evergreen-finanzas.ml/api/asset',
            {
              description: this.description,
              value: this.value,
              type: this.type,
            }
          )
          .then((res) => {
            this.$emit('assetCreated', true);
            console.log(res);
          })
          .catch((err) => console.log(err));
      } else {
        alert('Incorrect Asset Data');
      }
    },
  },
};
</script>
