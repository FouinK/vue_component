<script>

  import axios from "axios";

  export default {
      name: 'restAPI',
      methods: {
          getData() {
              const config = {
                  headers: {
                  },params: {
                      order: 'ADMIN_SETTING',
                  },
              };

              this.name = '회원가입 완료 !';
              alert("회원가입이 완료 되었습니다");

              axios.get('https://shop-api.e-ncp.com/display/banners/001', config)
                  .then((result) => {
                      console.log(result);
                      this.data = result;
                  });
          },
      },
      data() {
          return {
              data: {},

          }
      }
  }
</script>

<template>
  <main>
      {{name}}
      <div>
          <input placeholder="아이디"><br>
          <input placeholder="비밀번호" type="password"><br>
          <button @click="getData">Join</button>
      </div>
  </main>
</template>

<style scoped>

</style>