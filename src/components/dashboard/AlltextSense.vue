<template>
  <div id="all-text-sense">
    <h4 class="text-center">Emotion</h4>
    <wordcloud
      v-b-modal.modal-scrollable
      class="wordcloud"
      :data="defaultWords"
      nameKey="word"
      valueKey="count"
      :color="Accent"
      :showTooltip="true"
      :wordClick="wordClickHandler"
    ></wordcloud>

    <b-modal id="modal-scrollable" ok-only size="lg" scrollable>
      <template v-slot:modal-title>
        <h3>
          #
          <code>{{name}}</code>
          <code>{{filter}}</code>
        </h3>
      </template>

      <div class="card">
        <div class="card-body">
          <!-- Main table element -->
          <b-table show-empty small stacked="md" :items="item" :fields="fields" :filter="filter"></b-table>
        </div>
      </div>
    </b-modal>
  </div>
</template>

<script>
import wordcloud from "vue-wordcloud";

export default {
  name: "all-text-sense",
  components: {
    wordcloud,
  },
  methods: {
    wordClickHandler(name) {
      this.name = name;
      this.filter = name;
    },
  },

  data: () => ({
    name: "null",
    defaultWords: [
      { word: "ช่วย", count: 60 },
      { word: "ชายหาด", count: 59 },
      { word: "ป่า", count: 18 },
      { word: "น้ำ", count: 18 },
      { word: "ตอง", count: 16 },
      { word: "หาด", count: 15 },
      { word: "อาหาร", count: 12 },
      { word: "คน", count: 12 },
      { word: "เก้าอี้", count: 11 },
      { word: "กิจกรรม", count: 9 },
      { word: "ร้านอาหาร", count: 8 },
      { word: "ราคา", count: 7 },
      { word: "บาท", count: 7 },
      { word: "ถนน", count: 7 },
      { word: "ร่ม", count: 7 },
      { word: "เครื่องดื่ม", count: 6 },
      { word: "พระอาทิตย์", count: 6 },
      { word: "เวลา", count: 6 },
      { word: "ท้องถิ่น", count: 5 },
      { word: "ประเทศ", count: 5 },
      { word: "บาร์", count: 4 },
      { word: "ร้านค้า", count: 4 },
      { word: "เจ็ทสกี", count: 4 },
      { word: "ลา", count: 4 },
      { word: "ครอบครัว", count: 3 },
      { word: "เซล", count: 3 },
      { word: "มหาด", count: 3 },
      { word: "ลูก", count: 3 },
      { word: "เกาะ", count: 3 },
      { word: "โลก", count: 3 },
      { word: "โรงแรม", count: 3 },
      { word: "ทะเล", count: 3 },
      { word: "ร้าน", count: 3 },
      { word: "ตัวเลือก", count: 2 },
      { word: "ริมถนน", count: 2 },
      { word: "โอกาส", count: 2 },
      { word: "หิน", count: 2 },
      { word: "คลื่น", count: 2 },
      { word: "เตียง", count: 2 },
      { word: "อาบแดด", count: 2 },
      { word: "ร่มเงา", count: 2 },
      { word: "เลา", count: 2 },
      { word: "นจ์", count: 2 },
      { word: "มุม", count: 2 },
      { word: "ริ", count: 2 },
      { word: "สระน้ำ", count: 2 },
      { word: "กล้วย", count: 2 },
      { word: "กีฬา", count: 2 },
      { word: "ไอศ", count: 2 },
      { word: "ครีม", count: 2 },
      { word: "ยา", count: 2 },
      { word: "กระโดดร่ม", count: 2 },
      { word: "รถเข็น", count: 2 },
      { word: "ตลาด", count: 2 },
      { word: "ลูกชาย", count: 2 },
      { word: "ดวงอาทิตย์", count: 2 },
      { word: "จุด", count: 2 },
      { word: "ข้อมูล", count: 1 },
      { word: "เน็ต", count: 1 },
      { word: "สงบ", count: 1 },
      { word: "ทำเล", count: 1 },
      { word: "หยุดพัก", count: 1 },
      { word: "ปาร์ตี้", count: 1 },
      { word: "นัด", count: 1 },
      { word: "เดท", count: 1 },
      { word: "ฉาก", count: 1 },
      { word: "บอนด์", count: 1 },
      { word: "กิโลเมตร", count: 1 },
      { word: "สวรรค์", count: 1 },
      { word: "ค่า", count: 1 },
      { word: "รน", count: 1 },
      { word: "กะ", count: 1 },
      { word: "นโยบาย", count: 1 },
      { word: "สูบบุหรี่", count: 1 },
      { word: "รสชาติ", count: 1 },
      { word: "เค", count: 1 },
      { word: "บับ", count: 1 },
      { word: "ไก่", count: 1 },
      { word: "ไม้", count: 1 },
      { word: "แพทริค", count: 1 },
      { word: "รอยสัก", count: 1 },
      { word: "แปด", count: 1 },
      { word: "ขนาด", count: 1 },
      { word: "แว่นตา", count: 1 },
      { word: "เครื่องประดับ", count: 1 },
      { word: "รีวิว", count: 1 },
      { word: "คาด", count: 1 },
      { word: "กลางคืน", count: 1 },
      { word: "สินค้า", count: 1 },
      { word: "ข้อ", count: 1 },
      { word: "ฟรี", count: 1 },
      { word: "หัว", count: 1 },
      { word: "พัทยา", count: 1 },
      { word: "ชื่อ", count: 1 },
      { word: "ตง", count: 1 },
      { word: "รองเท้าแตะ", count: 1 },
      { word: "พริบตา", count: 1 },
      { word: "ตอนกลางคืน", count: 1 },
      { word: "คลับ", count: 1 },
      { word: "ฝักบัว", count: 1 },
      { word: "ห้องน้ำ", count: 1 },
      { word: "คนรัก", count: 1 },
      { word: "เก้า", count: 1 },
      { word: "ต้น", count: 1 },
      { word: "หมู่", count: 1 },
      { word: "ร้านกาแฟ", count: 1 },
      { word: "สัปดาห์", count: 1 },
      { word: "จอห์น", count: 1 },
      { word: "เงียบสงบ", count: 1 },
      { word: "คืน", count: 1 },
      { word: "เครื่องเล่น", count: 1 },
      { word: "แล่น", count: 1 },
      { word: "ลิง", count: 1 },
      { word: "ห้อง", count: 1 },
      { word: "เจ็ต", count: 1 },
      { word: "สกี", count: 1 },
      { word: "ลูกสาว", count: 1 },
      { word: "แพนเค้ก", count: 1 },
      { word: "คู่รัก", count: 1 },
      { word: "ประเภท", count: 1 },
      { word: "เย็น", count: 1 },
      { word: "เวีย", count: 1 },
      { word: "กลิ่น", count: 1 },
      { word: "พัก", count: 1 },
      { word: "โอ", count: 1 },
      { word: "รีสอร์ท", count: 1 },
      { word: "ขี่", count: 1 },
      { word: "ทริป", count: 1 },
      { word: "ร่มชูชีพ", count: 1 },
      { word: "พ่อค้า", count: 1 },
      { word: "ยอดเยี่ยม", count: 1 },
      { word: "เอเชีย", count: 1 },
      { word: "อาหารทะเล", count: 1 },
      { word: "มื้อ", count: 1 },
      { word: "มื้อค่ำ", count: 1 },
      { word: "อากาศ", count: 1 },
      { word: "เดือน", count: 1 },
      { word: "ตอน", count: 1 },
      { word: "แออัด", count: 1 },
      { word: "หลานสาว", count: 1 },
      { word: "ขยะ", count: 1 },
      { word: "สา", count: 1 },
      { word: "อายุ", count: 1 },
      { word: "ขวบ", count: 1 },
      { word: "พึมพำ", count: 1 },
      { word: "ทัศนคติ", count: 1 },
      { word: "sh * t", count: 1 },
      { word: "เออ", count: 1 },
      { word: "เบล", count: 1 },
      { word: "ผ้าเช็ดตัว", count: 1 },
      { word: "จอง", count: 1 },
      { word: "ค่าธรรมเนียม", count: 1 },
      { word: "ตัว", count: 1 },
      { word: "สิทธิพิเศษ", count: 1 },
      { word: "ภาษา", count: 1 },
      { word: "แสงอาทิตย์", count: 1 },
      { word: "ผิว", count: 1 },
      { word: "เสื้อผ้า", count: 1 },
      { word: "ห้า", count: 1 },
      { word: "กิโลกรัม", count: 1 },
      { word: "เอ็ด", count: 1 },
      { word: "แคนาดา", count: 1 },
      { word: "ร้านขายยา", count: 1 },
      { word: "ฝูง", count: 1 },
      { word: "วัว", count: 1 },
      { word: "รูเล็ต", count: 1 },
      { word: "ชีวิต", count: 1 },
      { word: "น้ำเงิน", count: 1 },
      { word: "วิว", count: 1 },
      { word: "เมือง", count: 1 },
      { word: "กองขยะ", count: 1 },
      { word: "ร่างกาย", count: 1 },
      { word: "เกลียด", count: 1 },
      { word: "คนขาย", count: 1 },
      { word: "เบียร์", count: 1 },
      { word: "ยอดนิยม", count: 1 },
      { word: "เล่นกีฬา", count: 1 },
      { word: "ผจญภัย", count: 1 },
    ],
    item: [
      {
        Review:
          "Different from the information in the net, the beach is clean, calm ans nice for families. İt is easy accessible, with a lot of options for cheap and tasty street food.",
        Name: "Panar Kyazim",
        Address: "-",
        Time: "Date of experience: January 2020",
        Rating: 5,
        Thai:
          "แตกต่างจากข้อมูลในเน็ตชายหาดสะอาดสงบและดีสำหรับครอบครัว มันสามารถเข้าถึงได้ง่ายมีตัวเลือกมากมายสำหรับอาหารริมถนนราคาถูกและอร่อยชายหาด",
      },
      {
        Review:
          "A busy but exciting beach with plenty of exiting opportunities for sports etc. Excellent local restaurants and bars, shops etc.",
        Name: "iann990",
        Address: "Edinburgh, United Kingdom",
        Time: "Date of experience: January 2020",
        Rating: 4,
        Thai:
          "ชายหาดที่วุ่นวาย แต่น่าตื่นเต้นพร้อมโอกาสมากมายสำหรับการเล่นกีฬา ฯลฯ ร้านอาหารและบาร์ท้องถิ่นที่ยอดเยี่ยมร้านค้า ฯลฯ ตอง",
      },
      {
        Review:
          "Besides the location not much going for it especially as there are so many fantastic beaches all around Patong and Phuket in general.",
        Name: "Susan Firth Bernard Kavanagh",
        Address: "Island of Malta, Malta",
        Time: "Date of experience: January 2020",
        Rating: 1,
        Thai:
          "นอกจากทำเลที่ตั้งไม่ค่อยไปโดยเฉพาะอย่างยิ่งเพราะมีชายหาดที่ยอดเยี่ยมมากมายรอบ ๆ ป่าตองและภูเก็ตโดยทั่วไปป่า",
      },
      {
        Review:
          "Patong Beach was absolutely amazing.  There are a bunch of restaurants that will provide you with great food and some shade when you need a break from the water.  Jet skis, parasailing and various water activities also await you here.  I was here for New Years Eve and the beach…",
        Name: "krich0311",
        Address: "Phoenix, Arizona",
        Time: "Date of experience: January 2020",
        Rating: 5,
        Thai:
          "หาดป่าตองเป็นสิ่งที่น่าอัศจรรย์อย่างยิ่ง มีร้านอาหารมากมายที่จะช่วยให้คุณได้รับอาหารอร่อยและร่มเงาเมื่อคุณต้องการหยุดพักจากน้ำ เจ็ทสกีพาราเซลลิ่งและกิจกรรมทางน้ำมากมายรอคุณอยู่ที่นี่ ฉันอยู่ที่นี่เพื่อปีใหม่และชายหาด",
      },
      {
        Review:
          "The beach and restaurants are ok, don’t come here for a relaxing holiday. Come here when you want to party and to date. The area has very nice places to visit. The traffic is busy and the distances to the nice sceneries to visit James Bond rock it’s about 100 km.",
        Name: "Ghentfreak",
        Address: "Hanoi, Vietnam",
        Time: "Date of experience: January 2020",
        Rating: 3,
        Thai:
          "ชายหาดและร้านอาหารโอเคอย่ามาที่นี่สำหรับวันหยุดพักผ่อนที่ผ่อนคลาย มาที่นี่เมื่อคุณต้องการปาร์ตี้และนัดเดท พื้นที่มีสถานที่ที่ดีมากในการเยี่ยมชม การจราจรไม่ว่างและระยะทางไปยังฉากที่ดีในการเยี่ยมชมหินบอนด์เจมส์มันอยู่ห่างออกไปประมาณหนึ่งร้อยกิโลเมตร",
      },
    ],

    fields: [
      {
        key: "Thai",
        label: "Review",
      },
    ],
    filter: null,
  }),
};
</script>

<style scoped>
.wordcloud {
  font-family: "Lato", Arial, sans-serif;
  width: 100%;
  height: 370px;
}
.right {
  text-align: right;
}
</style>