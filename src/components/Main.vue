<template>
  <div>
          {{data[1].children.length }}
      <div class="div1">
        <a-table :columns="columnsMain" :data-source="shortData" bordered>

        </a-table>
      </div>
      <div class="div2">
      </div>
  </div>
</template>

<script>
const txml = require('txml')
export default {
  name: 'Data',
  props: {
  },
  data: function () {
    return {
      data: null,
      product: null,
      shortData: null,
      sku: null,
      columnsMain: [
        {
          title: 'SKU',
          name: 'sku',
          dataIndex: 'children[0].children[0]',
          key: 'children[0]'
        },
        {
          title: 'Price',
          name: 'Price',
          dataIndex: 'children[5].children[0]',
          key: 'children[0]'
        },
      ],
      columnsSide: [
        {
          title: 'SKU',
          name: 'sku',
          dataIndex: 'children[0].children[0]',
          key: 'children[0]'
        },
        {
          title: 'Price',
          name: 'Price',
          dataIndex: 'children[5].children[0]',
          key: 'children[0]'
        },
      ]
    }
  },
  created () {
    this.getData ()
  },
  methods: {
    getData () {
        var self = this
        fetch('').then(function(resp) {
          return resp.text()
        }).then(function(data) {
          let parser = new DOMParser(),
          xmlDoc = parser.parseFromString(data, 'text/xml')
          console.log(xmlDoc.getElementsByTagName('PRODUCT')[0].getElementsByTagName('PRICE')[0].innerHTML)
          console.log(txml.parse(data))
          self.data = txml.parse(data)
          self.shortData = self.data[1].children
          console.log(self.shortData[0].children[5].children[0])
          console.log(self.shortData)
        })
    }
  }
}
</script>

<style>
.div1 {
  width: 69%;
  top: 10%
}
.div2 {
  padding-left: 69%;
  width: 29%;
  margin-left: 2%
}
</style>
