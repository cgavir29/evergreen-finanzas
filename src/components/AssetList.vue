<template>
  <div class="has-text-centered mt-6">
    <b-table
      class="mb-4"
      :data="tableData"
      :columns="columns"
      :selected.sync="selected"
    />

    <div class="has-text-centered">
      <b-button
        class="mr-3"
        label="Clear Selected"
        type="is-info"
        :disabled="!selected"
        @click="selected = null"
      />
      <b-button
        label="Delete Selected"
        type="is-danger"
        :disabled="!selected"
        @click="deleteAsset()"
      />
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  props: ['newAsset'],
  watch: {
    newAsset: function() {
      this.fetchAssets();
    },
  },
  data() {
    const tableData = [];

    return {
      tableData,
      selected: tableData[1],
      columns: [
        {
          field: 'id',
          label: 'ID',
          numeric: true,
        },
        {
          field: 'description',
          label: 'Description',
          centered: true,
        },
        {
          field: 'value',
          label: 'Value',
          centered: true,
        },
        {
          field: 'type',
          label: 'Type',
          centered: true,
        },
        {
          field: 'createdAt',
          label: 'Created At',
          centered: true,
        },
      ],
    };
  },
  beforeMount() {
    this.fetchAssets();
  },
  methods: {
    fetchAssets() {
      axios
        .get(
          'https://be.evergreen-finanzas.ml/api/asset'
        )
        .then((res) => {
          res.data.forEach(
            (asset) =>
              (asset.createdAt = new Date(asset.createdAt).toUTCString())
          );

          this.tableData = res.data;
        })
        .catch((err) => console.log(err));
    },
    deleteAsset() {
      axios
        .delete(
          'https://be.evergreen-finanzas.ml/api/asset/' +
            this.selected.id
        )
        .then((res) => {
          this.fetchAssets();
          console.log(res);
        })
        .catch((err) => console.log(err));
    },
  },
};
</script>
