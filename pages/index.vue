<style scoped>
input {
  -webkit-appearance: textfield;
  background-color: white;
  -webkit-rtl-ordering: logical;
  cursor: text;
  padding: 1px;
  border-width: 2px;
  border-style: inset;
  border-color: initial;
  border-image: initial;
}
user agent stylesheet input,
textarea,
select,
button {
  text-rendering: auto;
  color: initial;
  letter-spacing: normal;
  word-spacing: normal;
  text-transform: none;
  text-indent: 0px;
  text-shadow: none;
  display: inline-block;
  text-align: start;
  margin: 0em;
  font: 400 13.3333px Arial;
}

user agent stylesheet input,
textarea,
select,
button,
meter,
progress {
  -webkit-writing-mode: horizontal-tb !important;
}

.search {
  width: 100%;
  height: 80px;
}
.ivu-icon {
  color: blue;
}
.search-box {
  font: 14px/38px PingFangSC-Regular, '-apple-system', Simsun;
  width: 326px;
  height: 40px;
  padding: 0 11px;
}
.submit-input {
  position: absolute;
  clip: rect(0 0 0 0);
}
label {
  cursor: pointer;
}
.search-btn {
  float: right;
  width: 40px;
  height: 40px;
  text-align: center;
  background-color: #bf2c24;
}
.search-btn em {
  font-size: 18px;
  display: block;
  margin-top: 10px;
  color: #fff;
}
.iconfont {
  font-family: qd_iconfont !important;
  font-size: 24px;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -webkit-text-stroke-width: 0.1px;
  -moz-osx-font-smoothing: grayscale;
}
</style>

<template>
  <div class="search">
    <Row type="flex" justify="center">
      <div>
        <input class="search-box" id="s-box" name="kw" type="text" placeholder="这里有妖气" autocomplete="off">
        <input class="submit-input" type="submit" id="searchSubmit" data-eid="qd_A13">
        <label id="search-btn" class="search-btn" for="searchSubmit">
          <em class="iconfont" data-eid="qd_A13">
            <icon color="white" size="25" type="ios-search" />
          </em>
        </label>
      </div>
    </Row>
    <Row>

    </Row>
  </div>
</template>
<script>
export default {
  data() {
    return {
      search: ''
    }
  }
}
</script>
