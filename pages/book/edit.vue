<style scoped>
.mail_title {
  color: #2d8cf0;
  font-weight: bolder;
  font-size: 20px;
}
.mail_box {
  width: 100%;
  margin: 40px 0;
}
.border {
  width: 100%;
  border: 1px solid;
  color: #f5f7f9;
}
sideBar-group {
  margin: 0 0 20px;
}
li,
ol,
ul {
  padding: 0;
}
.sideBar-group li {
  font-size: 14px;
  line-height: 36px;
  position: relative;
  cursor: pointer;
  color: #3e3d43;
  border: 1px solid transparent;
  border-radius: 4px;
}

li {
  list-style: none;
}
.sideBar-group li .sideBar-list-a {
  display: block;
  overflow: hidden;
  padding: 0 20px;
  white-space: nowrap;
  text-overflow: ellipsis;
  border-radius: 4px;
}

.sideBar-group li.active {
  font-weight: 600;
  color: #ee4259;
  border: 1px solid #e0deda;
  background: #fff;
}
a {
  transition: color 0.3s;
  text-decoration: none;
  color: inherit;
}
</style>

<template>
  <div style="width:100%">
    <div class="mail_box">
      <Row type="flex" justify="center" align="top">
        <Col span="3">
        <ul class="sideBar-group">
          <li :class="active" @mouseover="selectStyle() " @mouseout="outStyle()">
            <a href="/bookcase/auto" class="sideBar-list-a" title="自动订阅" data-eid="qd_M188"> 编辑书籍</a>
          </li>
        </ul>
        </Col>
        <Col span="13" offset="1">
        <Card>
          <Form ref="form" :model="form" :rules="ruleValidate" label-position="left" :label-width="100">
            <FormItem label="书籍名称" prop="bookName">
              <Input v-model="form.bookName"></Input>
            </FormItem>
            <FormItem label="书籍代码" prop="bookID">
              <Input v-model="form.bookID"></Input>
            </FormItem>
            <FormItem label="追读章节" prop="bookChapter">
              <Input v-model="form.bookChapter"></Input>
            </FormItem>
            <FormItem>
              <Button type="primary" @click="handleSubmit('form')">提交</Button>
              <Button type="ghost" @click="handleReset('form')" style="margin-left: 8px">重置</Button>
            </FormItem>
          </Form>
        </Card>
        </Col>
      </Row>
    </div>
  </div>

</template>
<script>
export default {
  name: 'book-edit',
  data() {
    return {
      form: {
        bookName: '帝霸',
        bookID: '8_8109',
        bookChapter: '第3230章自作孽'
      },
      active: 'active',
      ruleValidate: {
        bookName: [
          {
            required: true,
            message: 'The bonk name cannot be empty',
            trigger: 'blur'
          }
        ],
        bookID: [
          {
            required: true,
            message: 'The book NO. cannot be empty',
            trigger: 'blur'
          }
        ],
        bookChapter: [
          {
            required: true,
            message: 'The chapter cannot be empty',
            trigger: 'blur'
          }
        ]
      }
    }
  },
  methods: {
    handleSubmit(name) {
      this.$refs[name].validate(valid => {
        if (valid) {
          this.$axios
            .post('/edit_book', {
              id: this.$route.params.id,
              name: this.form.bookName,
              book_no: this.form.bookID,
              chapter: this.form.bookChapter
            })
            .then(res => {
              if (res) {
                this.$Message.success('Success!')
              } else {
                this.$Message.error('Fail!')
              }
            })
        } else {
          this.$Message.error('Fail!')
        }
      })
    },
    handleReset(name) {
      this.$refs[name].resetFields()
    },
    selectStyle() {
      this.active = 'active'
    },
    outStyle() {
      //   this.active = ''
    }
  },
  mounted() {
    this.$axios.get('/book/' + this.$route.params.id).then(res => {
      if (res) {
        this.form.bookName = res.data.name
        this.form.bookChapter = res.data.chapter
        this.form.bookID = res.data.book_no
      }
    })
  }
}
</script>

