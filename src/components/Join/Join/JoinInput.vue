<template>
  <div class="join-input-container">
    <h2>회원가입</h2>

    <div class="join-input-form-container">
      <div class="join-input-form-item">
        <label>이메일*</label>
        <input type="email" id="id" placeholder="이메일을 입력해주세요" v-model="dataSet.email" @change="validateEmail(dataSet.email)">
      </div>
      <div class="join-input-form-item">
        <label>비밀번호*</label>
        <input type="password" id="pw" placeholder="비밀번호를 입력해주세요" v-model="dataSet.password" @change="validatePassword(dataSet.password, dataSet.passCheck)">
        <span>* 8자리 이상의 비밀번호를 설정해주세요</span>
      </div>
      <div class="join-input-form-item">
        <label>비밀번호 확인*</label>
        <input type="password" id="pw-check" placeholder="비밀번호를 한번 더 입력해주세요" v-model="dataSet.passCheck" @change="validatePassword(dataSet.password, dataSet.passCheck)">
      </div>
      <div class="join-input-form-item">
        <label>이름*</label>
        <input type="text" id="name" placeholder="반드시 실명을 기재해주세요" v-model="dataSet.name">
      </div>
      <div class="join-input-form-item">
        <label>휴대폰 번호*</label>
        <input type="tel" id="phone" placeholder="- 없이 입력해주세요" v-model="dataSet.phoneNumber" @change="validatePhoneNumber(dataSet.phoneNumber)">
      </div>

      <!-- delete -->
      <div class="join-input-form-item">
        <label>생년월일*</label>
        <input type="num" id="birth" placeholder="ex. 20220101" v-model="dataSet.birth" @change="validateBirthDate(dataSet.birth)">
      </div>

      <div class="join-input-form-item">
        <label>가입경로*</label>
        <div class="join-input-inflow-col-container">
          <div class="join-input-inflow-col-item">
            <div class="join-input-inflow-item">
              <input type="radio" name="from" id="everytime" value="EVERYTIME" v-model="dataSet.funnel">
              <label for="everytime">에브리타임</label> 
            </div>
            <div class="join-input-inflow-item">
              <input type="radio" name="from" id="kakaotalk" value="KAKAO" v-model="dataSet.funnel">
              <label for="kakaotalk">카카오톡 단톡방</label> 
            </div>
            <div class="join-input-inflow-item">
              <input type="radio" name="from" id="google" value="GOOGLE" v-model="dataSet.funnel">
              <label for="google">구글 검색</label> 
            </div>
            <div class="join-input-inflow-item">
              <input type="radio" name="from" id="naver" value="NAVER_SEARCH" v-model="dataSet.funnel">
              <label for="naver">네이버 검색</label> 
            </div>
            <div class="join-input-inflow-item">
              <input type="radio" name="from" id="instagram" value="INSTAGRAM" v-model="dataSet.funnel">
              <label for="instagram">인스타그램</label> 
            </div>
            <div class="join-input-inflow-item">
              <input type="radio" name="from" id="etc" value="ETC" v-model="dataSet.funnel">
              <label for="etc">기타</label> 
            </div>
          </div>

          <div class="join-input-inflow-col-item">
            <div class="join-input-inflow-item">
              <input type="radio" name="from" id="blog" value="NAVER_BLOG" v-model="dataSet.funnel">
              <label for="everytime">네이버 블로그</label> 
            </div>
            <div class="join-input-inflow-item">
              <input type="radio" name="from" id="지식in" value="NAVER_IN" v-model="dataSet.funnel">
              <label for="지식in">네이버 지식인</label> 
            </div>
            <div class="join-input-inflow-item">
              <input type="radio" name="from" id="cafe" value="NAVER_CAFE" v-model="dataSet.funnel">
              <label for="cafe">네이버 카페</label> 
            </div>
            <div class="join-input-inflow-item">
              <input type="radio" name="from" id="email" value="AD_EMAIL" v-model="dataSet.funnel">
              <label for="e-mail">이메일 홍보</label> 
            </div>
            <div class="join-input-inflow-item">
              <input type="radio" name="from" id="offline" value="AD_OFFLINE" v-model="dataSet.funnel">
              <label for="offline">오프라인 홍보</label> 
            </div>
            <div class="join-input-inflow-item">
              <input type="radio" name="from" id="acquaintance" value="ACQUAINTANCE" v-model="dataSet.funnel">
              <label for="acquaintance">지인 추천</label> 
            </div>
          </div>
        </div>
      </div>

      <div class="join-input-form-item">
        <label>상세 가입경로*</label>
        <input type="text" id="inflow-detail" placeholder="해당 가입경로에 대한 상세 내용을 작성해주세요" v-model="dataSet.funnel_detail">
        <span>* 검색 유입인 경우 검색어, 에브리타임/카카오톡/네이버 카페인 경우 소속을 알려주세요.</span>
      </div>

      <div class="join-input-form-item">
        <label>이용약관*</label>
        <div class="join-input-terms-container">
          <div class="join-input-terms-item">
            <input class="form-check-input" type="checkbox" v-model="checkAll">
            <label class="form-check-label" for="checkAll">전체 동의하기</label>
          </div>
          <div class="join-input-terms-item">
            <input class="form-check-input" type="checkbox" v-model="dataSet.check1">
            <label class="form-check-label"><a href="https://surveasy.oopy.io/terms-of-use" target="_blank">서베이지 이용약관 (필수)</a>
            </label>
          </div>
          <div class="join-input-terms-item">
            <input class="form-check-input" type="checkbox" v-model="dataSet.check2">
            <label class="form-check-label"><a href="https://surveasy.oopy.io/privacy-policy" target="_blank">서베이지 개인정보 보호 방침 (필수)</a>
            </label>
          </div>
          <div class="join-input-terms-item">
            <input class="form-check-input" type="checkbox" v-model="dataSet.check3">
            <label class="form-check-label">회원가입 시 작성한 개인 정보가 모두 올바름을 확인합니다. 가입 오류로 인한 불이익은 이용자의 책임임을 인지하고 있습니다. (필수)
            </label>
          </div>
        </div>
      </div>


    </div>
    
    <div class="join-input-button-container">
      <button id="btn-join" @click="signUp(dataSet)">회원가입하기</button>
    </div>
  </div>
</template>

<script>
import { instance } from '../../../api/index'
import { getAuth,  createUserWithEmailAndPassword } from 'firebase/auth'
import { setDoc, doc, getFirestore } from 'firebase/firestore';
export default {
  data(){
    return{
        dataSet:{
          email:null,
          password:null,
          passCheck:null,
          phoneNumber:null,
          name:null,
          // inflow:null,
          // inflow_detail:null,
          funnel:null,
          funnel_detail:null,
          check1: false,
          check2: false,
          check3: false,
        },
        validReg : false,
        validEmail : false,
        validPassword : false,
        validPhoneNumber : false,
        validBirthDate : false
    }
  },
  computed: {
    checkAll: {
      get: function() {
        return this.check1 && this.check2 && this.check3 
      },
      set: function(check) {
        if (check == true) {
          this.dataSet.check1 = true;
          this.dataSet.check2 = true;
          this.dataSet.check3 = true;
        } else {
          this.dataSet.check1 = false;
          this.dataSet.check2 = false;
          this.dataSet.check3 = false;
        }
      }
    }
  },
  methods: {
    validateEmail(email) {
      const result = /^[A-Za-z0-9_\\.\\-]+@[A-Za-z0-9\\-]+\.[A-Za-z0-9\\-]+/
      this.validEmail = result.test(email)
    },

    validatePassword(pw, pwCheck) {
      var pwLength = (pw.length >= 8)
      var pwSame = (pw == pwCheck)
      this.validPassword = pwLength && pwSame
    },

    validatePhoneNumber(phoneNumber) {
      this.validPhoneNumber = (phoneNumber.length >= 11 && isNaN(phoneNumber) == false)
    },

    validateBirthDate(date) {
      this.validBirthDate = ((date.length == 8) && date < 20230000)
    },

    validateSignUp(dataSet) {
      var errCode = [];
      if (this.hasNullOption(dataSet)) {
        alert("입력하지 않은 항목이 있습니다.")
      } else {
        if (!this.validPassword){
        // if (dataSet.password !== dataSet.passCheck){
          errCode.push(2)
        }
        //휴대폰번호 숫자만있는지 확인 (#Todo)
        if(!this.validPhoneNumber){
        // if((dataSet.phoneNumber).length<11 || isNaN(dataSet.phoneNumber)==true || (dataSet.phoneNumber).includes('.')==true){
          errCode.push(4)
        }
        if(!(dataSet.check1 ==true && dataSet.check2 ==true && dataSet.check3 ==true)){
          errCode.push(6)
        }
        if (errCode.length == 0 ){
          this.validReg = true
          return true
        } else {
          var registerErrorMessage =[
          "",
          "입력하지 않은 항목이 있습니다.",
          "비밀번호를 확인해주세요.",
          "비밀번호는 8자 이상이여야 합니다.",
          "휴대폰 번호를 올바르게 입력하세요.",
          "",
          "약관에 동의해주세요."
          ]
          var errAlert =[]
          for(var i=0; i<errCode.length; i++){
              errAlert.push(registerErrorMessage[errCode[i]])
              
          }
          var msg = ''
          for(var err in errAlert){
              msg+=errAlert[err]+"\n"
          }
          alert(msg) //에러코드에 해당하는 내용 띄우기
          return false
        }
      }

    },

    hasNullOption(dataSet) {
      if (dataSet.email == null || dataSet.password == null || dataSet.passCheck == null || dataSet.phoneNumber == null || dataSet.name == null || dataSet.funnel == null || dataSet.funnel_detail == null || dataSet.funnel_detail == "") {
        return true
      } else {
        return false
      }
    },

    signUp(data) {
      const validResult = this.validateSignUp(data);
      if (validResult) {
        const auth = getAuth();
        createUserWithEmailAndPassword(auth, data.email, data.password)
        .then((userCredential) => {
          const user = userCredential.user;
          this.$router.push('/login')
          this.createFirebaseUserData(data);
        })
        .catch((error) => {
          const errcode = error.code;
          if(error.code=="auth/email-already-in-use") {
              this.error = "이미 가입된 계정입니다."
              alert(this.error)
          }
          if(error.code=="auth/invalid-email") {
              this.error = "이메일 형식이 맞는지 확인해주세요."
              alert(this.error)
          }
        })
      } else {
      }
    },

    async createFirebaseUserData(data) {
      const db = getFirestore()
      await setDoc(doc(db, "userData",data.email.toString()), {
        name: data.name,
        email: data.email,
        phoneNumber: data.phoneNumber,
        isPanel: false,
        birth: data.birth,
        uploadIndex: [],
        identity: '할인 대상이 아닙니다.',
        identity_request: false,
        identity_responded: false,
        funnel : data.funnel,
        funnel_detail : data.funnel_detail,
        respondArray: [],
        clientGrade: 0,
        point_total : 0,
        point_current: 0,
        marketingSMS: false,
        marketingEmail: false
      });
      
    },

    // 서버 회원가입
    async signUpLater() {
      const validResult = this.validateSignUp(this.dataSet);
      
      if (validResult) {
        try {
          const response = await instance.post(
            '/user/signup',
            {
              email: this.dataSet.email,
              password: this.dataSet.password,
              name : this.dataSet.name,
              phoneNumber : this.dataSet.phoneNumber,
              inflowPath : this.dataSet.inflow,
              inflowPathDetail : this.dataSet.inflow_detail
            }
          )
          if(response.status == 200) {
            console.log(response.data)
            this.$router.push('/login')
          }else{
            console.log(response.data)
          }
        }catch(error){
          console.log(error)
        }
      }
    },


  }
}
</script>

<style>
.join-input-form-container {
  display: flex;
  flex-direction: column;
}
.join-input-form-item {
  display: flex;
  flex-direction: column;
  width: 400px;
  margin: 12px auto;
}
.join-input-form-item label {
  text-align: left;
  font-size: 14px;
  font-weight: bold;
  margin-bottom: 3px;
}
.join-input-form-container input {
  height: 50px;
  padding-left: 10px;
  color: #727272;
  background-color: white;
  border: solid 1px #dadada;
  border-radius: 5px;
}
.join-input-form-container input:focus {
  color: #000000;
  outline: 1px solid #0AAC00;
}
.join-input-form-item span {
  color: #0AAC00;
  text-align: left;
  font-size: 10px;
  margin-top: 2px;
}
.join-input-inflow-container span {
  text-align: left;
}
.join-input-inflow-col-container {
  display: flex;
  flex-direction: row;
  margin-top: 5px;
}
.join-input-inflow-item {
  display: flex;
  flex-direction: row;
  width: 180px;
  align-items: center;
}
.join-input-inflow-item label {
  width: 80%;
  font-weight: 500;
  margin: auto;
}
.join-input-inflow-item input {
  height: 30px;
}
.join-input-inflow-item input:focus {
  outline: none;
}
.join-input-terms-container {
  align-items: left;
}
.join-input-terms-item {
  display: flex;
  flex-direction: row;
}
.join-input-terms-item input {
  height: 20px;
  margin-top: 3px;
}
.join-input-terms-item input:focus {
  outline: none;
}
.join-input-terms-item label {
  width: 100%;
  font-size: 14px;
  font-weight: 500;
  color: #6e6e6e;
  margin: auto;
}
.join-input-terms-item a {
  color: #6e6e6e;
}
.join-input-button-container {
  display: flex;
  flex-direction: column;
  margin: 15px 0 20px 0;
}
.join-input-button-container button {
  width: 400px;
  height: 40px;
  margin: 5px auto;
  border: none;
  border-radius: 7px;
  cursor: pointer;
}
#btn-join {
  background-color: #0AAC00;
  color: white;
  border: solid 1px #0AAC00;
}

</style>