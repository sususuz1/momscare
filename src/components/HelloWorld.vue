<template>
  <div v-if="check == 0" class="login_wrap bgc">
    <div class="login_title"><span>맘스케어 상담카드</span></div>
    <div class="login">
      <input
        v-model="inputId"
        type="text"
        placeholder="생년월일 6자리 (예:930629)"
      />
      <div class="login_btn" @click="check_ID()">
        <span>상담카드 조회</span>
      </div>
    </div>
  </div>

  <div v-else>
    <div><DrugCard /></div>
  </div>
</template>

<script>
import DrugCard from "./DrugCard.vue";

let userId = "930629";

export default {
  mounted() {
    // var onlyUrl = window.location.href;
    // var targetURL = onlyUrl.slice(0, onlyUrl.indexOf("/mom"));
    // var imgpath = targetURL + "/image/";
  },
  components: {
    DrugCard,
  },
  data: function () {
    return {
      inputId: "",
      check: 0,
    };
  },

  methods: {
    check_ID() {
      if (this.inputId == userId) this.check = 1;
      else this.check = 0;
    },
  },
};
</script>

<style>
.login_wrap {
  display: flex;
  justify-content: center;

  height: 100vh;
  align-items: center;
}
.login_title {
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  border-bottom: 1px solid #ccc;
  height: 50px;
  font-weight: bold;
}
.login input {
  height: 40px;
  width: 320px;
  border: none;
  border-bottom: 1px solid #eee;
  margin-bottom: 10px;
  padding-left: 20px;
}
input::placeholder {
  text-align: center;
  font-size: 15px;
}
.login_btn {
  background-color: #fdd017;
  height: 35px;
  padding: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 5px;
}
</style>
