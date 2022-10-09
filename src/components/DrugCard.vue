<template>
  <div>
    <div class="header bgc">
      <span>약력관리 상담카드</span>
    </div>
    <div class="greetings bgc">
      <div>
        <span class="greetings_title">맘스케어약국은</span>· 정확하고 청결한
        조제와 <br />&nbsp;&nbsp;안전한 약물사용을 제 1가치로 여깁니다
        <div class="grettings_contents">
          · 약력관리 차트로 약의 변화를 확인하고 <br />&nbsp;&nbsp;약물 상호
          작용에 대한 상담 후 투약합니다
        </div>
        · 가장 좋은 약을 선정하는 것에 최선을 다합니다.
      </div>
    </div>
    <div class="side_effect bgc">
      <div class="side_effect_title">부작용 / 주의성분</div>
      <div>{{ DATA[0].status[0].SIDEEFFECT }}</div>
    </div>
    <div class="info bgc">
      <div class="info_title">
        <div></div>
        <div class="info_title_name"></div>
        <div></div>
      </div>
      <div class="info_hos_wrap">
        <div class="info_hos">
          <div>조제일자</div>
          <div>
            <span class="hos_color">{{ DATA[0].status[0].S_REGDATE }}</span>
          </div>
        </div>
        <div class="info_hos1">
          <div>병원</div>
          <div>
            <span class="hos_color">{{ DATA[0].status[0].HOSPITALNM }}</span>
          </div>
        </div>
        <div class="info_hos2">
          <div>진료과</div>
          <div>
            <span class="hos_color">{{ DATA[0].status[0].TREAT }}</span>
          </div>
        </div>
      </div>
    </div>

    <div class="contents">
      <!-- <div class="tab"><img src="../img/tap.png" /></div> -->
      <div v-for="(item, i) in data2" v-bind:key="item.id">
        <div
          class="drug_item bgc"
          @click="openModal(item, i)"
          v-if="item.DNAME"
        >
          <div class="redline" v-if="item.drug_as_met == 'aspirin'"></div>
          <div class="greenline" v-if="item.drug_as_met == 'metformin'"></div>
          <div class="grayline"></div>
          <!-- <div class="drug_img">
            <img :src="require(`../img/${item.drug_img}`)" class="drug_img" />
          </div> -->
          <div class="drug_img">
            <img :src="require(`../img/${item.DCODE}.jpg`)" class="drug_img" />
          </div>
          <!-- <div class="drug_name2">{{ item.DNAME }}</div> -->
          <div class="drug_name">
            &nbsp;&nbsp;&nbsp;{{ item.DNAME }}
            <div class="drug_date">
              <div class="margin">
                <div>투여량</div>
                <div>{{ item.DQUANTITY }}</div>
              </div>
              <div class="margin">
                <div>투약횟수</div>
                <div>{{ item.DCOUNT }}</div>
              </div>
              <div>
                <div>투여일</div>
                <div>{{ item.DDAY }}</div>
              </div>
            </div>
          </div>
          <div class="drug_check" v-if="item.drug_check">
            {{ item.drug_check }}
          </div>
          <div class="drug_button">약 설명 보기</div>
        </div>

        <div
          class="modal_wrap"
          v-if="modalVisible && modalIndex == i"
          :data="modalData"
          @click="modalVisibleControl()"
        >
          <div class="modal" @click="modalVisibleControl()">
            <div class="modal_com_wrap">
              <div class="drug_item bgc">
                <div
                  class="modal_redline"
                  v-if="item.drug_as_met == 'aspirin'"
                ></div>
                <div
                  class="modal_greenline"
                  v-if="item.drug_as_met == 'metformin'"
                ></div>
                <div class="modal_grayline"></div>
                <div class="drug_img">
                  <img
                    :src="require(`../img/${item.DCODE}.jpg`)"
                    class="drug_img"
                  />
                </div>
                <!-- <div class="drug_name2">{{ item.DNAME }}</div> -->
                <div class="drug_name">
                  &nbsp;&nbsp;&nbsp;{{ item.DNAME }}
                  <div class="drug_date">
                    <div class="margin">
                      <div>투여량</div>
                      <div>{{ item.DQUANTITY }}</div>
                    </div>
                    <div class="margin">
                      <div>투약횟수</div>
                      <div>{{ item.DCOUNT }}</div>
                    </div>
                    <div>
                      <div>투여일</div>
                      <div>{{ item.DDAY }}</div>
                    </div>
                  </div>
                </div>
                <div class="drug_check" v-if="item.drug_check">
                  {{ item.drug_check }}
                </div>
                <div class="drug_button drug_diff" v-if="item.drug_diff">
                  {{ item.drug_diff }}
                </div>
              </div>
            </div>
            <div class="metformin" v-if="item.drug_as_met == 'metformin'">
              조영제 사용 검사시 <br />이 약의 투여사실을 의료진에게 미리
              알리세요.
            </div>
            <div class="aspirin" v-if="item.drug_as_met == 'aspirin'">
              치과 치료, 내시경 검사시 ... 까먹음..
            </div>
            <div class="modal_url" v-if="item.drug_url">
              <iframe
                width="359"
                height="280"
                :src="`https://www.youtube.com/embed/${item.drug_url}`"
                title="YouTube video player"
                frameborder="0"
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                allowfullscreen
              ></iframe>
            </div>
            <div class="modal_drug_info_line">
              <div class="modal_drug_info_title">약품설명</div>
              <div class="modal_drug_info">
                <div v-if="item.drug_info1">· {{ item.drug_info1 }}</div>
                <div v-if="item.drug_info2">· {{ item.drug_info2 }}</div>
                <div v-if="item.drug_info3">· {{ item.drug_info3 }}</div>
                <div v-if="item.drug_info4">· {{ item.drug_info4 }}</div>
              </div>
            </div>
            <div class="picto">
              <div class="picto_aspirin" v-if="item.drug_as_met == 'aspirin'">
                <img src="../img/pic_aspirin.jpg" />
              </div>
            </div>
            <div class="modal_close" @click="modalVisibleControl()">닫기</div>
          </div>
        </div>
      </div>
    </div>
    <div class="footer bgc">
      맘스케어약국 <br />
      테스트중
    </div>
    <div class="modal_height"></div>
  </div>
</template>

<script>
// import axios from "axios";
export default {
  mounted() {
    window.scrollTo(0, 0);

    this.DATA[0].status[0].HOSPITALNM =
      this.DATA[0].status[0].HOSPITALNM.replace("☆", "");
    this.DATA[0].status[0].HOSPITALNM =
      this.DATA[0].status[0].HOSPITALNM.replace("★", "");

    /* eslint-disable */
    var reg = /\(([^)]+)\)/;
    /* eslint-enable */

    var apiData = this.DATA[0].status[0];

    var list = [];
    var objectkeys = [
      "DCODE",
      "DNAME",
      "DQUANTITY",
      "DCOUNT",
      "DCHANGE",
      "DDAY",
    ];
    var regex = /[^0-9]/g;
    Object.keys(apiData).map((data) => {
      objectkeys.map((key) => {
        if (data.indexOf(key) !== -1) {
          var number = +data.replace(regex, "");
          if (!list[number]) list[number] = {};
          list[number][key] = apiData[data];
        }
      });
    });

    console.log(list);
    this.data2 = list;
    let i;
    for (i = 0; i < 10; i++) {
      if (this.data2[i].DNAME != null)
        this.data2[i].DNAME = this.data2[i].DNAME.replace(reg, "");
    }

    // var sYYMMDD = "a";
    // var onlyUrl = window.location.href;
    // var targetURL = onlyUrl.slice(0, onlyUrl.indexOf("/mom"));

    // const url = new URL(
    //   "http://happymomscare.shop/momscare.html?key=c2021041600116649820000900099187IaM7ZmU6riw64K06rO8"
    // );
    // const urlParams = url.searchParams;
    // document.write(urlParams.get("key") + "<br>");

    // axios
    //   .get(targetURL + ":5811/" + urlParams + "==" + sYYMMDD)
    //   .then(function (response) {
    //     console.log(response);
    //   })
    //   .catch(function (error) {
    //     console.log(error);
    //   });
  },

  data: function () {
    return {
      modalVisible: false,
      modalData: null,
      // aspirin: false,
      // metformin: false,
      data2: [],
      DATA: [
        {
          status: [
            {
              code: "r20221006003",
              S_REGDATE: "2022/10/06",
              SIDEEFFECT: "테스트1",
              HOSPITALNM: "☆분당제생병원",
              TREAT: "소화기내과",
              DCODE0: "d20140228064",
              DNAME0: "판토록정40(pantoprazole위산분비억제제)",
              DQUANTITY0: 1,
              DCOUNT0: 1,
              DDAY0: 56,
              DCHANGE0: "신규추가",
              DCODE1: "d20170103001",
              DNAME1: "가스티인씨알정15(mosapride기능성소화)",
              DQUANTITY1: 1,
              DCOUNT1: 1,
              DDAY1: 56,
              DCHANGE1: "신규추가",
              DCODE2: "d20210711001",
              DNAME2: "무코스타서방정150(rebamipide위점막보호)",
              DQUANTITY2: 1,
              DCOUNT2: 2,
              DDAY2: 56,
              DCHANGE2: "신규추가",
              DCODE3: "d20140226104",
              DNAME3: "액사딘캡슐150(nizatidine위염)",
              DQUANTITY3: 1,
              DCOUNT3: 1,
              DDAY3: 56,
              DCHANGE3: "신규추가",
              DCODE4: "",
              DNAME4: "",
              DQUANTITY4: 0,
              DCOUNT4: 0,
              DDAY4: 0,
              DCHANGE4: "",
              DCODE5: "",
              DNAME5: "",
              DQUANTITY5: 0,
              DCOUNT5: 0,
              DDAY5: 0,
              DCHANGE5: "",
              DCODE6: "",
              DNAME6: null,
              DQUANTITY6: 0,
              DCOUNT6: 0,
              DDAY6: 0,
              DCHANGE6: "",
              DCODE7: "",
              DNAME7: null,
              DQUANTITY7: 0,
              DCOUNT7: 0,
              DDAY7: 0,
              DCHANGE7: "",
              DCODE8: "",
              DNAME8: null,
              DQUANTITY8: 0,
              DCOUNT8: 0,
              DDAY8: 0,
              DCHANGE8: "",
              DCODE9: "",
              DNAME9: null,
              DQUANTITY9: 0,
              DCOUNT9: 0,
              DDAY9: 0,
              DCHANGE9: "",
              QNA1: "★판토록)위산분비를 감소시켜 위십이지장궤양,역류질환,위산 과분비 상태 치료.",
              QNA2: "★판토록)하루의 첫 식사하기 30분 전에 복용하고, 30분후 식사를 해야 효과가 좋습니다.",
              QNA3: "★판토록)클로스트리디움 디피실레균성 설사 위험성 증가와 연관이 있으며, 설사가 지속시 참고합니다.",
              QNA4: "★판토록)1년이상 장기복용시 골다공증과 연관된 골절의 위험성이 증가할수 있습니다.",
              QNA5: "★(가스티인cr)기능성소화불량으로 인한소화기능이상을 치료합니다.공복에 복용합니다.",
              QNA6: "★(가스티인cr)소화관평활근운동을 촉진 물질을 분비하게해서, 소화관운동촉진하는 약입니다.",
              QNA7: "★(가스티인cr)약효가 서서히방출하는 제제이므로 자르지않고 통째로 삼킵니다.",
              QNA8: "★(무코스타)위장점막에서prostaglandin생성촉진,위점막보호,위점막혈류량증가,위점막세포성장촉진",
              QNA9: "★(무코스타)성인 1일2회 아침저녁으로1정씩복용. 통째로 삼켜야하며, 자르거나 씹지 않습니다.",
              QNA10:
                "★액사딘)위궤양,십이지장궤양,위식도역류질환에서 위산분비를 줄입니다.",
              CONSULT1:
                "*(무코스타)위점막병변(미란,출혈,발적,부종)개선,급성위염,만성위염의 급성악화기에 사용.",
              CONSULT2:
                "*(무코스타)위점막 보호작용과 궤양 치유 능력을 가진 약으로 위염,위궤양치료에 사용됩니다.",
              CONSULT3: "",
              CONSULT4: "",
              CONSULT5: "",
              CONSULT6: "",
              CONSULT7: "",
              CONSULT8: "",
              CONSULT9: "",
              CONSULT10: "",
            },
            {
              code: "r20220414115",
              S_REGDATE: "2022/04/14",
              SIDEEFFECT: "테스트2",
              HOSPITALNM: "☆분당제생병원",
              TREAT: "내분비내과",
              DCODE0: "d20131210004",
              DNAME0: "씬지로이드정0.05(levothyroxine갑상선약,핑크,차광보관)",
              DQUANTITY0: 1,
              DCOUNT0: 1,
              DDAY0: 182,
              DCHANGE0: "변화없음",
              DCODE1: "d20140812005",
              DNAME1: "암로닌정5(amlodipine고혈압,흰색팔각형Λ5,KMP)",
              DQUANTITY1: 1,
              DCOUNT1: 1,
              DDAY1: 182,
              DCHANGE1: "변화없음",
              DCODE2: "",
              DNAME2: null,
              DQUANTITY2: 0,
              DCOUNT2: 0,
              DDAY2: 0,
              DCHANGE2: "",
              DCODE3: "",
              DNAME3: null,
              DQUANTITY3: 0,
              DCOUNT3: 0,
              DDAY3: 0,
              DCHANGE3: "",
              DCODE4: "",
              DNAME4: null,
              DQUANTITY4: 0,
              DCOUNT4: 0,
              DDAY4: 0,
              DCHANGE4: "",
              DCODE5: "",
              DNAME5: null,
              DQUANTITY5: 0,
              DCOUNT5: 0,
              DDAY5: 0,
              DCHANGE5: "",
              DCODE6: "",
              DNAME6: null,
              DQUANTITY6: 0,
              DCOUNT6: 0,
              DDAY6: 0,
              DCHANGE6: "",
              DCODE7: "",
              DNAME7: null,
              DQUANTITY7: 0,
              DCOUNT7: 0,
              DDAY7: 0,
              DCHANGE7: "",
              DCODE8: "",
              DNAME8: null,
              DQUANTITY8: 0,
              DCOUNT8: 0,
              DDAY8: 0,
              DCHANGE8: "",
              DCODE9: "",
              DNAME9: null,
              DQUANTITY9: 0,
              DCOUNT9: 0,
              DDAY9: 0,
              DCHANGE9: "",
              QNA1: "★씬지로이드)갑상선기능저하정,점액부종,크레틴병,단순성 갑상선종을 치료합니다.",
              QNA2: "★씬지로이드)아침식전1시간에드시고 다른약은 아침식후드시거나,철분제는 자기전에드세요.",
              QNA3: "★암로닌)혈관을 확장하여 전신 혈관저항을 떨어트려 혈압을 낮춥니다.",
              QNA4: "★암로닌)심장의 부담을 줄여주며, 심장으로의 산소공급을 늘려 협심증을 치료합니다.",
              QNA5: "★암로닌)부작용은 홍조,말초부종, 두통 등 입니다.",
              QNA6: "★암로닌)자몽주스는 이약의 효과를 올리므로 드시지 마세요.",
              QNA7: "",
              QNA8: "",
              QNA9: "",
              QNA10: "",
              CONSULT1:
                "김, 미역,다시마 같은 해조류,어패류 등을 적정량 포함한 균형식을 권해요.",
              CONSULT2:
                "즙,달인 물, 액기스, 환, 가루와 같은 형태의 섭취는 피하세요.",
              CONSULT3:
                "고혈압)체중감량10kg시 혈압5~20mmHg을 줄일수 있습니다.가장확실하게 혈압을낮춥니다.",
              CONSULT4:
                "고혈압)염분 섭취를 제한하세요.(소금 6g(표시된나트륨량x2.5배)이하를 목표)2~8mmhg줄임",
              CONSULT5:
                "고혈압)술의 섭취를 제한(맥주1~2캔,소주1~2잔,포도주120~240㎖)2~4mmhg줄임",
              CONSULT6: "",
              CONSULT7: "",
              CONSULT8: "",
              CONSULT9: "",
              CONSULT10: "",
            },
          ],
        },
      ],
      users: { side_effect: "알러지" },
      drugs: [
        {
          drug_name: "아스피린프로텍트정100",
          drug_img: "A1.jpg",
          drug_check: "항혈소판제",
          drug_as_met: "aspirin",
          drug_url: "",
          drug_num1: "1",
          drug_num2: "1",
          drug_num3: "90",
          drug_diff: "신규추가",
          drug_info1:
            "혈소판이 혈전에 붙어서 색전이 되어 혈관을 막는것을 예방하는 약입니다.",
          drug_info2:
            "수술전,임플란트발치,내시경예정시 처방의께 며칠중단할지 확인합니다.",
        },
        {
          drug_name: "플라비톨정75",
          drug_img: "A2.jpg",
          drug_check: "고지혈증",
          drug_as_met: "aspirin",
          drug_url: "",
          drug_num1: "1",
          drug_num2: "2",
          drug_num3: "90",
          drug_diff: "신규추가",
          drug_info1:
            "뇌경색,심근경색환자에서 죽상동맥경화성 증상을 개선합니다.",
          drug_info2:
            "심혈관계 이상으로 인한 사망줄이고,심근경색예방,뇌경색 허혈을 개선 합니다.",
          drug_info3:
            "심방세동인 경우 뇌졸중포함 죽상혈전증, 혈전색전증 위험성을 감소시킵니다.",
          drug_info4:
            "임플란트,내시경,수술시 며칠 중단할 지 주치의께 확인합니다.",
        },
        {
          drug_name: "메트포민서방정",
          drug_img: "A3.jpg",
          drug_check: "당뇨약",
          drug_as_met: "metformin",
          drug_url: "",
          drug_num1: "1",
          drug_num2: "2",
          drug_num3: "90",
          drug_diff: "신규추가",
          drug_info1:
            "미각장애, 위장 장애를 줄이기 위해 식사 직후에 복용하는 것이 좋습니다.",
          drug_info2: "혈당 조절에 지장을 줄 수 있으므로 술은 피하세요.",
          drug_info3:
            "조영술,ct시 사용 요오드조영제와 상호작용있으므로 검사 이틀전 의사에게 알립니다.",
          drug_info4:
            "매운음식,어지러움,소화불량의 부작용이 있는경우 비타민B12결핍의 증상일수 있습니다.",
        },
        {
          drug_name: "트레스탄캡슐",
          drug_img: "A4.jpg",
          drug_check: "식욕촉진제",
          drug_as_met: "",
          drug_url: "",
          drug_num1: "1",
          drug_num2: "2",
          drug_num3: "90",
          drug_diff: "신규추가",
          drug_info1: "심방세동으로인한 뇌졸중,전신색전증위험을 감소시킵니다.",
          drug_info2:
            "식사와 함께복용합니다.음식에의해 생체이용률이 상승합니다.치과,내시경수술시말씀하세요",
          drug_info3:
            "자몽주스를 마시지않습니다.clarithromycin병용시 자렐토약효증가주의.",
          drug_info4:
            "출혈의 징후(소변의피,코피,객혈,잇몸출혈,두통,어지러움)가 있으면 의사에게 알리세요",
        },
        {
          drug_name: "알포콜린리드캡슐",
          drug_img: "A5.jpg",
          drug_check: "고양이",
          drug_as_met: "",
          drug_url: "",
          drug_num1: "1",
          drug_num2: "1",
          drug_num3: "180",
          drug_diff: "신규추가",
          drug_info1: "뇌의 신경전달작용을 향상시킵니다.",
          drug_info2:
            "기억력저하,방향감각장애,자발성저하, 집중력 감소를 개선합니다.",
          drug_info3: "구역,구토등이 심하면 의사에게 알리세요.",
          drug_info4: "",
        },
        {
          drug_name: "쿨프렙산",
          drug_img: "A6.jpg",
          drug_check: "대장세척",
          drug_as_met: "",
          drug_url: "https://youtu.be/H_GdJo8ScC0?t=75",
          drug_num1: "1",
          drug_num2: "1",
          drug_num3: "1",
          drug_diff: "신규추가",
          drug_info1: "뇌의 신경전달작용을 향상시킵니다.",
          drug_info2:
            "기억력저하,방향감각장애,자발성저하, 집중력 감소를 개선합니다.",
          drug_info3: "구역,구토등이 심하면 의사에게 알리세요.",
          drug_info4: "",
        },
        {
          drug_name: "렐바200엘립타",
          drug_img: "A7.jpg",
          drug_check: "대장세척",
          drug_as_met: "",
          drug_url: "https://youtu.be/pj9AMd5Tg-Y?t=106",
          drug_num1: "1",
          drug_num2: "1",
          drug_num3: "1",
          drug_diff: "신규추가",
          drug_info1: "뇌의 신경전달작용을 향상시킵니다.",
          drug_info2:
            "기억력저하,방향감각장애,자발성저하, 집중력 감소를 개선합니다.",
          drug_info3: "구역,구토등이 심하면 의사에게 알리세요.",
          drug_info4: "",
        },
      ],
    };
  },
  props: ["item"],
  methods: {
    openModal(data, i) {
      this.modalIndex = i;
      this.modalData = data;
      this.modalVisible = true;
      this.drugs[i].drug_url = this.drugs[i].drug_url.replace(
        "https://youtu.be/",
        ""
      );
      let positionTop = window.scrollY || document.documentElement.scrollTop;
      document.body.className = "overflow";

      document.body.style.top = `-${positionTop}px`;
    },
    modalVisibleControl() {
      this.modalVisible = false;
      document.body.classList.remove("overflow");
      document.body.style.top = `${this.positionTop}px`;
    },
  },
};
</script>

<style>
/* font */
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans+KR&display=swap");
body {
  font-family: "Noto Sans KR", sans-serif;
  /* background-color: rgb(252, 252, 252); */
  background-color: rgb(248, 248, 248);
}

.bgc {
  background-color: #fff;
}

div {
  box-sizing: border-box;
}

.overflow {
  overflow: hidden;
  height: 100%;
  width: 100%;
  position: fixed;
}
/* header */
.header {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100px;
  /* border-bottom: 1px solid #eee; */
  box-shadow: 0px 2px 5px #eee;
  margin-bottom: 7px;
  font-weight: bold;
  font-size: 25px;
  text-align: center;
}
/* info */
.info,
.side_effect,
.greetings {
  border-top: 1px solid #eee;
  border: 1px solid #eee;
  margin-top: 10px;
  margin-bottom: 10px;
  padding: 10px 0px;
  box-shadow: 0px 2px 5px #eee;
  border-radius: 5px;
  margin-left: 5px;
  margin-right: 5px;
}

.side_effect,
.greetings {
  padding-left: 10px;
  padding-right: 10px;
  padding-bottom: 15px;
}

.greetings_title {
  display: block;
  margin-bottom: 8px;
  font-weight: bold;
}
.grettings_contents {
  margin: 7px 0;
  border-top: 1px solid #eee;
  border-bottom: 1px solid #eee;
  padding: 7px 0;
}
.side_effect_title {
  border-bottom: 1px solid #eee;
  padding-bottom: 5px;
  margin-bottom: 5px;
  color: rgb(73, 107, 172);
  font-size: 16px;
}
.info_title {
  display: flex;
  justify-content: space-between;
}
.info_title_name {
  /* border-bottom: 2px solid rgb(235, 235, 235); */
  color: rgb(41, 41, 41);
}
.info_hos_wrap {
  padding: 10px;
}
.info_hos,
.info_hos1,
.info_hos2 {
  display: flex;
  justify-content: space-between;
}
.hos_color {
  color: rgb(73, 107, 172);
}
/* drug_list */
.drug_img {
  width: 160px;
  display: flex;
}
.drug_item {
  /* border: 1px solid #eee; */

  display: flex;
  padding: 5px 2px;
  margin-bottom: 5px;
  border-radius: 5px;
  margin: 10px 5px;
  position: relative;
  padding-bottom: 18px;
}
.drug_img {
  margin-right: 7px;
  margin-top: 3px;
  margin-left: 4px;
}
.drug_name {
  width: 100%;
  color: rgb(73, 107, 172);
  font-weight: bold;
  margin-top: 0px;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
.drug_name2 {
  width: 100%;
  color: rgb(73, 107, 172);
  font-weight: bold;
  position: absolute;
  top: 0;
  left: 0;
  padding-top: 3px;
  padding-left: 11px;
  padding-bottom: 5px;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
.drug_date {
  width: 90%;
  margin: 0 auto;
  text-align: center;
  border-top: 1px solid #eee;
  border-bottom: 1px solid #eee;
  color: black;
  font-weight: 400;
  display: flex;
  justify-content: center;
  font-size: 14px;
  margin-top: 6px;
}

.drug_date .margin {
  margin-right: 15px;
}

.drug_check {
  color: rgb(161, 76, 76);
}

/* modal */
.modal_wrap {
  background-color: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 999;
  overflow: auto;
}

.modal_box {
  position: relative;
  height: 100%;
  padding: 10px;
}

.modal {
  background-color: #fff;
  width: 100%;

  margin-top: 10px;
  border-radius: 8px;
  padding-bottom: 10px;
  box-shadow: 1px 3px 3px rgba(0, 0, 0, 0.4);
  overflow: auto;
  margin-bottom: 10px;
}
.modal_drug_name {
  color: rgb(73, 107, 172);
  font-weight: bold;
  text-align: center;

  margin: 0 auto;
  display: block;
}
.modal_drug_img {
  margin: 0 auto;

  width: 200px;
  padding-top: 10px;
}
.modal_drug_img img {
  margin: 0 auto;
}

.modal_close {
  margin: 0 auto;
  width: 50px;
  text-align: center;
  border: 1px solid #eee;
  padding: 0px 5px;
  box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.5);
  border-radius: 4px;
  margin-top: 30px;
  margin-bottom: 10px;
  /* position: absolute;


  left: 150px;
  bottom: 10px; */
  background-color: rgb(248, 248, 248);
}
.modal_close_top {
  width: 100px;
  margin: 0 auto;
  text-align: center;
  border: 1px solid #eee;
  padding: 5px 10px;
  box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.5);
  border-radius: 4px;
  margin-top: 10px;
  margin-bottom: 10px;

  background-color: rgb(248, 248, 248);
}

.modal_drug_info_title {
  padding: 10px;
}
.modal_drug_info {
  width: 100%;

  padding: 10px;
}
.modal_drug_info div {
  margin-bottom: 10px;
  font-size: 14px;
  border-bottom: 1px solid #eee;
  padding-bottom: 10px;
}

.modal_com_wrap {
  padding-top: 5px;
}

.picto {
  width: 100%;
  display: flex;
  justify-content: center;
}

.picto_aspirin img {
  width: 100px;
}

.metformin {
  margin: 5px;
  padding: 10px;
  border: 1px solid rgb(150, 196, 173);
  font-size: 16px;
  border-radius: 5px;
}
.aspirin {
  margin: 5px;
  padding: 10px;
  border: 1px solid rgb(231, 148, 148);
  font-size: 16px;
  border-radius: 5px;
}
.modal_url {
  margin: 5px;
  padding: 10px;
  border: 1px solid #eee;
  font-size: 16px;
  border-radius: 5px;
}
.drug_button,
.drug_check {
  position: absolute;
  bottom: 7px;
  right: 6px;
  border: 1px solid rgb(209, 209, 209);
  padding: 0px 6px;
  border-radius: 4px;
}
.drug_check {
  margin-right: 100px;
  width: 90px;
  text-align: center;
}

.drug_diff {
  color: rgb(235, 122, 122);
  padding: 0px 15px;
}

.footer {
  border-top: 1px solid #eee;
  border: 1px solid #eee;
  margin-top: 10px;
  margin-bottom: 10px;
  padding: 10px 0px;
  box-shadow: 0px 2px 5px #eee;
  border-radius: 5px;
  margin-left: 5px;
  margin-right: 5px;
  text-align: center;
}
.redline,
.modal_redline {
  border: 1px solid rgb(231, 148, 148);
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 4px;
}
.greenline,
.modal_greenline {
  border: 1px solid rgb(150, 196, 173);
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 4px;
}
.grayline,
.modal_grayline {
  border: 1px solid #eee;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 4px;
}

/* media query */

@media screen and (min-width: 367px) and (max-width: 376px) {
  .drug_img {
  }
  .drug_check,
  .drug_button {
    font-size: 14px;
    padding: 2px 3px;
  }
  .drug_check {
    margin-right: 82px;
    width: 90px;
  }
}
@media screen and (max-width: 366px) {
  .greetings,
  .drug_name,
  .drug_date {
    font-size: 14px;
  }
  .drug_img {
    width: 130px;
    height: 80px;
  }
  .drug_date {
    font-size: 12px;
  }
  .drug_check,
  .drug_button {
    font-size: 14px;
    padding: 0px 3px;
  }
  .drug_check {
    margin-right: 82px;
    width: 78px;
  }
  iframe {
    border: 1px solid red;
    width: 298px;
  }
}
</style>
