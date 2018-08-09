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
            <a href="/bookcase/auto" class="sideBar-list-a" title="自动订阅" data-eid="qd_M188"> 邮箱编辑</a>
          </li>
        </ul>
        </Col>
        <Col span="14" offset="1">
        <Card>
          <!-- <p slot="title">
                        <span class="mail_title">邮箱设置</span>
                    </p> -->
          <Form ref="form" :model="form" :rules="ruleValidate" label-position="left" :label-width="100">
            <FormItem label="SMTP邮箱" prop="smtpHost">
              <Input v-model="form.smtpHost"></Input>
            </FormItem>
            <FormItem label="SMTP端口" prop="smtpPort">
              <Input v-model="form.smtpPort"></Input>
            </FormItem>
            <FormItem label="邮箱账号" prop="email">
              <Input v-model="form.email"></Input>
            </FormItem>
            <FormItem label="授权码" prop="pwd">
              <Input v-model="form.pwd" type="password"></Input>
            </FormItem>
            <FormItem label="KINDLE地址" prop="Kemail">
              <Input v-model="form.Kemail"></Input>
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
  data() {
    return {
      id: '',
      form: {
        smtpHost: '',
        smtpPort: '',
        email: '',
        pwd: '',
        Kemail: ''
      },
      active: 'active',
      ruleValidate: {
        smtpHost: [
          {
            required: true,
            message: 'The smtpHost cannot be empty',
            trigger: 'blur'
          }
        ],
        smtpPort: [
          {
            required: true,
            message: 'The smtpPort cannot be empty',
            trigger: 'blur'
          }
        ],
        pwd: [
          {
            required: true,
            message: 'The password cannot be empty',
            trigger: 'blur'
          }
        ],
        email: [
          {
            required: true,
            message: 'Mailbox cannot be empty',
            trigger: 'blur'
          },
          { type: 'email', message: 'Incorrect email format', trigger: 'blur' }
        ],
        Kemail: [
          {
            required: true,
            message: 'Mailbox cannot be empty',
            trigger: 'blur'
          },
          { type: 'email', message: 'Incorrect email format', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    handleSubmit(name) {
      let url = '/new_mail'
      if (this.id) {
        url = '/edit_mail'
      }
      this.$refs[name].validate(valid => {
        if (valid) {
          this.$axios
            .post(url, {
              uid: '1',
              smtpHost: this.form.smtpHost,
              smtpPort: this.form.smtpPort,
              mail: this.form.email,
              pwd: this.form.pwd,
              kindlEmail: this.form.Kemail
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
    this.$axios.get('/mail/1').then(res => {
      if (res) {
        let data = res.data
        this.form.smtpHost = data.smtphost
        this.form.smtpPort = data['smtpport']
        this.form.email = data['mail']
        this.form.pwd = data['pwd']
        this.id = data['id']
        this.form.Kemail = data['kindlemail']
      }
    })
  }
}
</script>

