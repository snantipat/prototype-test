<template>
  <div>
    <h4 class="text-center">Action</h4>
    <wordcloud
    v-b-modal.modal-scrollableVerb
      class="wordcloud"
      :data="defaultWords"
      nameKey="word"
      valueKey="count"
      :color="Accent"
      :showTooltip="true"
      :wordClick="wordClickHandlerVerb"
    ></wordcloud>

   
</div>


</template>

<script>

import wordcloud from "vue-wordcloud";
export default {
  name: "common-word-cloud-vreb",
  components: {
    wordcloud,

  },

  data: () => ({
    name:null ,
    defaultWords: [
   

      { word: "ชม ", count: 6 },
      { word: "แออัด ", count: 6 },
      { word: "ดู ", count: 6 },
      { word: "เดิน ", count: 6 },
      { word: "ยอดเยี่ยม ", count: 5 },
      { word: "พักผ่อน ", count: 5 },
      { word: "สวยงาม ", count: 5 },
      { word: "ยุ่ง ", count: 5 },
      { word: "ตก ", count: 5 },
      { word: "พัก ", count: 5 },
      { word: "เยี่ยม ", count: 4 },
      { word: "ทำ ", count: 4 },
      { word: "เพลิดเพลิน ", count: 4 },
      { word: "วุ่นวาย ", count: 3 },
      { word: "ผ่อนคลาย ", count: 3 },
      { word: "สกปรก ", count: 3 },
      { word: "แน่ใจ ", count: 3 },
      { word: "ขาย ", count: 3 },
      { word: "สงบ ", count: 3 },
      { word: "ชายหาด ", count: 3 },
      { word: "ปลอดภัย ", count: 3 },
      { word: "เช่า ", count: 3 },
      { word: "หลีกเลี่ยง ", count: 2 },
     
      { word: "ซื้อ ", count: 2 },
      { word: "นั่ง ", count: 2 },
      { word: "*ดี ", count: 2 },
      { word: "ระวัง ", count: 2 },
      { word: "หยาบคาย ", count: 2 },
      { word: "อาบแดด ", count: 2 },
      { word: "เลวร้าย ", count: 2 },
      { word: "ตอง ", count: 2 },
      { word: "จอง ", count: 2 },
      { word: "เงียบสงบ ", count: 2 },
      { word: "กิน ", count: 2 },
      { word: "นวด ", count: 2 },
      { word: "เล่นกีฬา ", count: 1 },
      { word: "รอ ", count: 1 },
      { word: "โอเค ", count: 1 },
      { word: "เจมส์ ", count: 1 },
      { word: "รบกวน ", count: 1 },
      { word: "ปล่อย ", count: 1 },
      { word: "ประหลาดใจ ", count: 1 },
      { word: "รูสึก ", count: 1 },
      { word: "ตะ ", count: 1 },
      { word: "ห้าม ", count: 1 },
      { word: "ย่อ ", count: 1 },
      { word: "หมึก ", count: 1 },
      { word: "ประทับใจ ", count: 1 },
      { word: "ถาม ", count: 1 },
      { word: "*เหมือน ", count: 1 },
      { word: "นิยม ", count: 1 },
      { word: "เงียบ ", count: 1 },
      { word: "แน่น ", count: 1 },
      { word: "แพง ", count: 1 },
      { word: "คอย ", count: 1 },
      { word: "ร้องเรียน ", count: 1 },
      { word: "สั่ง ", count: 1 },
      { word: "สัมผัส ", count: 1 },
      { word: "ถอด ", count: 1 },
      { word: "เดินเล่น ", count: 1 },
      { word: "ระบุ ", count: 1 },
      { word: "แล่น ", count: 1 },
      { word: "เย่ ", count: 1 },
      { word: "บ้าคลั่ง ", count: 1 },
      { word: "สีขาว ", count: 1 },
      { word: "ริม ", count: 1 },
      { word: "ล่อง ", count: 1 },
      { word: "ลอย ", count: 1 },
      { word: "ตัดสินใจ ", count: 1 },
      { word: "วางแผน ", count: 1 },
      { word: "ดูแล ", count: 1 },
      { word: "เจ็ทสกี ", count: 1 },
      { word: "เก้าอี้ ", count: 1 },
      { word: "ลืม ", count: 1 },
      { word: "สะดวก ", count: 1 },
      { word: "สวย ", count: 1 },
      { word: "อบอุ่น ", count: 1 },
      { word: "*ประทับใจ ", count: 1 },
      { word: "ร่า ", count: 1 },
      { word: "แทน ", count: 1 },
      { word: "เดินทอดน่อง ", count: 1 },
      { word: "บลู ", count: 1 },
      { word: "เชี่ยน ", count: 1 },
      { word: "ดูเหมือน ", count: 1 },
      { word: "ฉีก ", count: 1 },
      { word: "แตก ", count: 1 },
      { word: "งดงาม ", count: 1 },
      { word: "ดึงดูด ", count: 1 },
      { word: "รักษา ", count: 1 },
      { word: "เกรซ ", count: 1 },
      { word: "แลนด์ ", count: 1 },
      { word: "ถน ", count: 1 },
      { word: "ทิ้ง ", count: 1 },
      { word: "คาดหวัง ", count: 1 },
      { word: "นอน ", count: 1 },
      { word: "ชอบ ", count: 1 },
      { word: "เร่งเร้า ", count: 1 },
      { word: "ปฏิเสธ ", count: 1 },
      { word: "*สนใจ ", count: 1 },
      { word: "*หยุดยั้ง ", count: 1 },
      { word: "ทำลาย ", count: 1 },
      { word: "ล่า ", count: 1 },
      { word: "วาง ", count: 1 },
      { word: "ผ้าเช็ดตัว ", count: 1 },
      { word: "ค้นหา ", count: 1 },
      { word: "ประหลาด ", count: 1 },
      { word: "*แพง ", count: 1 },
      { word: "แรง ", count: 1 },
      { word: "สีแทน ", count: 1 },
      { word: "ซักรีด ", count: 1 },
      { word: "วิเศษ ", count: 1 },
      { word: "หลบ ", count: 1 },
      { word: "เกาะ ", count: 1 },
      { word: "อุ่น ", count: 1 },
      { word: "เมืองไทย ", count: 1 },
      { word: "รู้สึก ", count: 1 },
      { word: "สนทนา ", count: 1 },
      { word: "คุ้มค่า ", count: 1 },
      { word: "เล่น ", count: 1 },
      { word: "ร้านอาหาร ", count: 1 },
      { word: "ลอง ", count: 1 },
      { word: "สนุก ", count: 1 },
      { word: "ลองดู ", count: 1 },
    ],
  }),
  methods: {
    wordClickHandlerVerb(name) {
      this.name = name;
    },
  },
};
</script>
<style  scoped>
.wordcloud{
  height: 250px;
}
 .position{
   margin: 30px;
 }
 .boder{
   border-radius: 30px;
   margin: 15px;
    box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 3px 10px 0 rgba(0, 0, 0, 0.19);
 }
</style>