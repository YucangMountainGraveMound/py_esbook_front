<template>
  <Row type="flex" justify="center" align="top">
    <Col span='16'>
    <Card>
      <Table border :columns="columns" :data="data"></Table>
    </Card>
    </Col>
  </Row>
</template>
<script>
export default {
  data() {
    return {
      columns: [
        {
          title: '书籍名称',
          key: 'name',
          render: (h, params) => {
            return h('div', [h('strong', params.row.name)])
          }
        },
        {
          title: '编号',
          key: 'book_no'
        },
        {
          title: '追读章节',
          key: 'chapter'
        },
        {
          title: '操作',
          key: 'action',
          width: 150,
          align: 'center',
          render: (h, params) => {
            return h('div', [
              h(
                'Button',
                {
                  props: {
                    type: 'primary',
                    size: 'small'
                  },
                  style: {
                    marginRight: '5px'
                  },
                  on: {
                    click: () => {
                      this.edit(params.row.id)
                    }
                  }
                },
                '编辑'
              ),
              h(
                'Button',
                {
                  props: {
                    type: 'error',
                    size: 'small'
                  },
                  on: {
                    click: () => {
                      this.remove(params.row.id)
                    }
                  }
                },
                '删除'
              )
            ])
          }
        }
      ],
      data: [
        {
          id: 1,
          name: '',
          book_no: '',
          chapter: ''
        }
      ]
    }
  },
  methods: {
    edit(index) {
      this.$router.push({ name: 'book-edit', params: { id: index } })
    },
    remove(index) {
      this.$axios.get('/del_book/' + index).then(res => {
        if (res) {
          this.$Message.success('Success!')
        } else {
          this.$Message.error('Fail!')
        }
      })
    }
  },
  mounted() {
    this.$axios.get('/all_book/1').then(res => {
      if (res) {
        this.data = res.data
      }
    })
  }
}
</script>