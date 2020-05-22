<template>
  <form @submit.prevent="submit">
    <input type="submit" value="导出"/>
  </form>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      user: {
        phone: '',
        type: ''
      }
    }
  },
  methods: {
    submit: function () {
      // 这里用axios原生的去请求
      axios({
        method: 'get',
        url: 'http://132.129.1.67:8080/quantization/user/excel/export/all',
        // headers里面设置token
        headers: {
          Authorization: 'Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX25hbWUiOiJhZG1pbiIsInNjb3BlIjpbInJlYWQiXSwiaWQiOjEsImV4cCI6MTU5MDE1NDg3NiwiYXV0aG9yaXRpZXMiOlsiUk9MRV9BRE1JTiJdLCJqdGkiOiI0YTk1ZTY1OC0zNDJmLTQ5YjAtYWZkOC1lYzU1ZWIyZGFkMzEiLCJjbGllbnRfaWQiOiJxdWFudGl6YXRpb24ifQ.Mv8wKkTm6YHQqCO8kUGg-tQGgiADARBAG9a2i-olQ0XEbHsJiqsrNknGQM41frIxCpgAQw3Fy_ADDNuu6MgTIS6SqzV2GER1pwGras287vMsJFG3PYQ7S_vuFPDcDkR2hbwdCEayFFsKFFKd2Y-DZMCo2CFHWrBqk-RTeakr37sUKeyf4VixGtqbx--TsNIENIzM9XskbN3p4neYOb8fuQtmrWMsdpgzQOSn6J_DseIDSvVg7CABL7YM9NfBmSo3RVEOosJlF9OQL8EIrpDEOwWy4lX41KVr77a0uOC7e4vhEKijspuWzPtTZUyfxKv9njYANlEk6FGnQ3cjGSKr_g'
        },
        // 二进制流文件，一定要设置成blob，默认是json
        responseType: 'blob'
      }).then(res => {
        console.log('返回结果：{}', res)
        // filename名称截取
        let temp = res.headers['content-disposition'].split(';')[1].split('=')[1]
        // 对文件名乱码转义--【Node.js】使用iconv-lite解决中文乱码
        let iconv = require('iconv-lite')
        iconv.skipDecodeWarning = true // 忽略警告
        let fileName = iconv.decode(temp, 'utf-8')
        console.log('fileName', fileName)
        const link = document.createElement('a')
        const blob = new Blob([res.data])
        link.style.display = 'none'
        link.href = URL.createObjectURL(blob)
        link.setAttribute('download', fileName)
        document.body.appendChild(link)
        link.click()
        document.body.removeChild(link)
      })
    }
  }
}
</script>
