<template>
  <div id="all-comment">
    <b-container fluid>
      <!-- User Interface controls -->
      <b-row>
        <b-col lg="6" class="my-1">
          <b-form-group
            label="Sort"
            label-cols-sm="3"
            label-align-sm="right"
            label-size="sm"
            label-for="sortBySelect"
            class="mb-0"
          >
            <b-input-group size="sm">
              <b-form-select v-model="sortBy" id="sortBySelect" :options="sortOptions" class="w-75">
                <template v-slot:first>
                  <option value>-- none --</option>
                </template>
              </b-form-select>
              <b-form-select v-model="sortDesc" size="sm" :disabled="!sortBy" class="w-25">
                <option :value="false">Asc</option>
                <option :value="true">Desc</option>
              </b-form-select>
            </b-input-group>
          </b-form-group>
        </b-col>

        <b-col lg="6" class="my-1">
          <b-form-group
            label="Filter"
            label-cols-sm="3"
            label-align-sm="right"
            label-size="sm"
            label-for="filterInput"
            class="mb-0"
          >
            <b-input-group size="sm">
              <b-form-input
                v-model="filter"
                type="search"
                id="filterInput"
                placeholder="Type to Search"
              ></b-form-input>
              <b-input-group-append>
                <b-button :disabled="!filter" @click="filter = ''">Clear</b-button>
              </b-input-group-append>
            </b-input-group>
          </b-form-group>
        </b-col>
        
        <b-col sm="5" md="6" class="my-1">
          <b-form-group
            label="Per page"
            label-cols-sm="6"
            label-cols-md="4"
            label-cols-lg="3"
            label-align-sm="right"
            label-size="sm"
            label-for="perPageSelect"
            class="mb-0"
          >
            <b-form-select v-model="perPage" id="perPageSelect" size="sm" :options="pageOptions"></b-form-select>
          </b-form-group>
        </b-col>

        <b-col sm="7" md="6" class="my-1">
          <b-pagination
            v-model="currentPage"
            :total-rows="totalRows"
            :per-page="perPage"
            align="fill"
            size="sm"
            class="my-0"
          ></b-pagination>
        </b-col>
      </b-row>


      <div id="space"></div>
      <div class="card">
        <div class="card-body">
          <!-- Main table element -->
          <b-table
            show-empty
            small
            stacked="md"
            :items="item"
            :fields="fields"
            :current-page="currentPage"
            :per-page="perPage"
            :filter="filter"
            :filterIncludedFields="filterOn"
            :sort-by.sync="sortBy"
            :sort-desc.sync="sortDesc"
            :sort-direction="sortDirection"
            @filtered="onFiltered"
          ></b-table>
        </div>
      </div>
    </b-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      item: [
        {
          Review:
            "Different from the information in the net, the beach is clean, calm ans nice for families. İt is easy accessible, with a lot of options for cheap and tasty street food.",
          Name: "Panar Kyazim",
          Address: "-",
          Time: "Date of experience: January 2020",
          Rating: 5,
          Thai:
            "แตกต่างจากข้อมูลในเน็ตชายหาดสะอาดสงบและดีสำหรับครอบครัว มันสามารถเข้าถึงได้ง่ายมีตัวเลือกมากมายสำหรับอาหารริมถนนราคาถูกและอร่อย",
        },
        {
          Review:
            "A busy but exciting beach with plenty of exiting opportunities for sports etc. Excellent local restaurants and bars, shops etc.",
          Name: "iann990",
          Address: "Edinburgh, United Kingdom",
          Time: "Date of experience: January 2020",
          Rating: 4,
          Thai:
            "ชายหาดที่วุ่นวาย แต่น่าตื่นเต้นพร้อมโอกาสมากมายสำหรับการเล่นกีฬา ฯลฯ ร้านอาหารและบาร์ท้องถิ่นที่ยอดเยี่ยมร้านค้า ฯลฯ",
        },
        {
          Review:
            "Besides the location not much going for it especially as there are so many fantastic beaches all around Patong and Phuket in general.",
          Name: "Susan Firth Bernard Kavanagh",
          Address: "Island of Malta, Malta",
          Time: "Date of experience: January 2020",
          Rating: 1,
          Thai:
            "นอกจากทำเลที่ตั้งไม่ค่อยไปโดยเฉพาะอย่างยิ่งเพราะมีชายหาดที่ยอดเยี่ยมมากมายรอบ ๆ ป่าตองและภูเก็ตโดยทั่วไป",
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
        {
          Review:
            "Not a nice beach, over crowded and dirty. Would definitely avoid if possible. But if that didn’t bother you than give it a go.",
          Name: "MickyC",
          Address: "Bromley, United Kingdom",
          Time: "Date of experience: January  2020",
          Rating: 2,
          Thai:
            "ไม่ใช่ชายหาดที่สวยงามแออัดและสกปรก จะหลีกเลี่ยงอย่างแน่นอนถ้าเป็นไปได้ แต่ถ้านั่นไม่ได้รบกวนคุณมากกว่าปล่อยมันไป",
        },
        {
          Review:
            "I was very surprised how clean the beach was and even over New Years it never felt too busy. Clear water. Some nice beach bars along the front too.",
          Name: "Davinajs",
          Address: "Island of Malta, Malta",
          Time: "Date of experience: December 2019",
          Rating: 5,
          Thai:
            "ฉันประหลาดใจมากที่ชายหาดสะอาดและแม้กระทั่งในช่วงปีใหม่มันไม่เคยรู้สึกยุ่งเกินไป น้ำใส. มีบาร์ริมหาดที่ดีอยู่ด้านหน้าเช่นกัน",
        },
        {
          Review:
            "Very beautiful beach but very crowded . Too many water excursion people and long tail boats .  Will Recommend Paradise Beach , the best beach in Phuket , there is entrance fee of 200 bahts bt its worth paying .  Should also visit Karon and Kata Beach , Very clear water and very…",
          Name: "Haresh",
          Address: "Benidorm, Spain",
          Time: "Date of experience: January 2020",
          Rating: 3,
          Thai:
            "ชายหาดที่สวยงามมาก แต่แออัดมาก คนเที่ยวน้ำมากเกินไปและเรือหางยาว จะแนะนำหาดสวรรค์ซึ่งเป็นชายหาดที่ดีที่สุดในจังหวัดภูเก็ตมีค่าเข้าชมสองร้อยบาท แต่มันคุ้มค่า ควรไปที่หาดกะรนและกะตะน้ำใสมาก ๆ",
        },
        {
          Review:
            "Great beach for relaxing and people watching. Beautifully clean, there is a no smoking policy in place on the beach now but plenty of smoking areas. Great food and drink stands catering for every taste. The chicken kebabs and the potato skewers are lovely. There are plenty of…",
          Name: "MeR",
          Address: "Northwood, United Kingdom",
          Time: "Date of experience: January 2020",
          Rating: 5,
          Thai:
            "ชายหาดที่ดีสำหรับการพักผ่อนและผู้คนที่ดู สะอาดอย่างสวยงามมีนโยบายห้ามสูบบุหรี่บนชายหาดตอนนี้ แต่พื้นที่สูบบุหรี่มากมาย อาหารและเครื่องดื่มที่ยอดเยี่ยมย่อมาจากอาหารทุกรสชาติ เคบับไก่และมันฝรั่งเสียบไม้น่ารัก มีมากมาย",
        },
        {
          Review:
            "We went to Celebrity Ink and were more than impressed Patrick went above and beyond to make sure everything went better than we could imagine . If you’re looking for a tattoo this is definitely the place to go !!",
          Name: "J smith",
          Address: "",
          Time: "Date of experience: January 2020",
          Rating: 5,
          Thai:
            "เราไปที่หมึกผู้มีชื่อเสียงและยิ่งใหญ่กว่าแพทริคที่ประทับใจไปเกินกว่าที่จะทำให้แน่ใจว่าทุกอย่างดีขึ้นกว่าที่เราจะจินตนาการได้ หากคุณกำลังมองหารอยสักนี่เป็นสถานที่ที่จะไปแน่นอน",
        },
        {
          Review:
            "We have been to Patong Beach many times with our children (18,13 & 8) and while it is a very busy place and you will be asked 100s of times if you want to buy something , it can still be a relaxing place. The surf is so small that the kids are safe to swim in it. You can sit…",
          Name: "Mandybb21",
          Address: "Australian Capital Territory, Australia",
          Time: "Date of experience: January  2020",
          Rating: 4,
          Thai:
            "เราเคยไปที่หาดป่าตองหลายครั้งกับลูก ๆ ของเรา 18,13 & แปดและในขณะที่มันเป็นสถานที่ที่วุ่นวายมากและคุณจะถูกถาม 100s ครั้งถ้าคุณต้องการซื้ออะไรก็ยังคงเป็นสถานที่ผ่อนคลาย คลื่นมีขนาดเล็กมากจนเด็ก ๆ สามารถว่ายน้ำได้อย่างปลอดภัย คุณสามารถนั่ง",
        },
        {
          Review:
            "Beach it itself is clean enough (unlike others I have visited in Thailand), but given an average score as prices are high for sunbed use, drinks and food. It is hard to relax due to the number of people trying to sell you sunglasses, jewellery and anything else you can think of",
          Name: "Katie H",
          Address: "Scunthorpe, United Kingdom",
          Time: "Date of experience: January 2020",
          Rating: 3,
          Thai:
            "ชายหาดมันสะอาดพอไม่เหมือนที่อื่น ๆ ที่ฉันเคยไปเที่ยวมาในประเทศไทย แต่ได้คะแนนเฉลี่ยเพราะราคาสูงสำหรับการใช้เตียงอาบแดดเครื่องดื่มและอาหาร มันยากที่จะผ่อนคลายเนื่องจากมีคนจำนวนหนึ่งที่พยายามขายแว่นตากันแดดเครื่องประดับและสิ่งอื่น ๆ ที่คุณนึกออก",
        },
        {
          Review:
            "It's the most popular beach in Phuket filled up with tourists till sunset. I would'nt recommend it to you if you are looking for some me time as it's always crowded but i won't give it a bad review for that as well.",
          Name: "SubhrajyotiC",
          Address: "Kolkata (Calcutta), India",
          Time: "Date of experience: November 2019",
          Rating: 5,
          Thai:
            "มีชายหาดที่เป็นที่นิยมมากที่สุดในจังหวัดภูเก็ตที่เต็มไปด้วยนักท่องเที่ยวจนถึงพระอาทิตย์ตก ฉันจะไม่แนะนำให้คุณถ้าคุณกำลังมองหาบางเวลาฉันเพราะมันแออัดเสมอ แต่ฉันจะไม่ให้รีวิวที่ไม่ดีสำหรับมันเช่นกัน",
        },
        {
          Review:
            "Bangla road is over-estimated and expensive. It is quiet in the morning and extremely busy and overcrowded at night. The saying: “ if it’s too loud, you are too old” - might be applicable, though my experience is: too loud, too busy and too expensive. Be careful: they sell fake…",
          Name: "Jan de Vos",
          Address: "-",
          Time: "Date of experience: December 2019",
          Rating: 3,
          Thai:
            "ถนนบางลาสูงเกินคาดและมีราคาแพง มันเงียบในตอนเช้าและยุ่งมากและแน่นเกินไปในเวลากลางคืน คำพูดที่ว่าถ้าดังเกินไปคุณจะแก่เกินไปอาจใช้ได้แม้ว่าประสบการณ์ของฉันจะดังเกินไปยุ่งเกินไปและแพงเกินไป ระวังพวกเขาขายของปลอม",
        },
        {
          Review:
            "Overcrowded with very rude Europeans unfortunately.. the typical Asian beach experience.FULL of sun loungers and people hounding you to purchase goods..",
          Name: "Sherie",
          Address: "Byron Bay, Australia",
          Time: "Date of experience: January 2020",
          Rating: 4,
          Thai:
            "แออัดไปด้วยชาวยุโรปที่หยาบคายมาก ประสบการณ์ชายหาดเอเชียทั่วไป เก้าอี้อาบแดดเต็มไปด้วยผู้คนคอยให้คุณซื้อสินค้า",
        },
        {
          Review:
            "If you are staying in Patong, this is an easy clean cute beach to access. Just a basic beach, must get there early if you want shade or a lounge chair. They need to add more chairs, that’s my only complaint. But for a free, local easy access beach. It works! Obviously, it’s…",
          Name: "Lisaj730",
          Address: "New York City, New York",
          Time: "Date of experience: January 2020",
          Rating: 4,
          Thai:
            "หากคุณพักในป่าตองนี่เป็นชายหาดที่น่ารักที่สะอาดและเข้าถึงได้ง่าย แค่ชายหาดธรรมดาต้องไปถึงก่อนถ้าคุณต้องการร่มเงาหรือเก้าอี้เลานจ์ พวกเขาจำเป็นต้องเพิ่มเก้าอี้มากขึ้นนั่นคือข้อร้องเรียนของฉันเท่านั้น แต่ฟรีชายหาดเข้าถึงได้ง่ายในท้องถิ่น มันใช้งานได้อย่างชัดเจนมันมี",
        },
        {
          Review:
            "Patong beach is one of the worst beaches I've been to in Thailand, as it's overcrowded with tourists and dirty. There were no nice food stands to order from, so it can't even touch beaches in Hua Hin, Pattaya and Koh Chang to name a few. Katong beach which is the nearest…",
          Name: "Pepijn Amoruso",
          Address: "Hua Hin, Thailand",
          Time: "Date of experience: January 2020",
          Rating: 2,
          Thai:
            "หาดป่าตองเป็นหนึ่งในชายหาดที่เลวร้ายที่สุดที่ฉันเคยไปมาในประเทศไทยเพราะมีนักท่องเที่ยวหนาแน่นและสกปรก ไม่มีอาหารที่ดีที่จะสั่งจากดังนั้นมันจึงไม่สามารถสัมผัสชายหาดในหัวหินพัทยาและเกาะช้างเพื่อชื่อไม่กี่ หาดกะตงซึ่งเป็นหาดที่ใกล้ที่สุด",
        },
        {
          Review:
            "Patong Beach  Patong  738012982  Of all the places in the world to take off my sandals and stroll the beach, this one is it. Simply stated, access to this beach is an eye blink from along the roadside where one finds Para sailing one of the most fascinating activities, along…",
          Name: "rcs_multiverse",
          Address: "Chalong, Thailand",
          Time: "Date of experience: June 2019",
          Rating: 4,
          Thai:
            "หาดป่าตองป่าตองเจ็ดแสนสามหมื่นแปดพันสองหมื่นเก้าแสนแปดหมื่นสองแห่งจากทั่วทุกมุมโลกที่จะถอดรองเท้าแตะของฉันแล้วเดินเล่นที่ชายหาดคนนี้แหละ ระบุไว้อย่างง่ายๆการเข้าถึงชายหาดแห่งนี้เป็นพริบตาจากริมถนนที่มีคนพบว่ามีการแล่นเรือใบหนึ่งในกิจกรรมที่น่าสนใจที่สุดตามมา",
        },
        {
          Review:
            "We spent NYE wandering along Bangla Road. What a wild and crazy atmosphere!  Not a place to bring your children, even on non holiday evenings/nights though.",
          Name: "Chuck D",
          Address: "Progreso, Mexico",
          Time: "Date of experience: December 2019",
          Rating: 4,
          Thai:
            "เราใช้เวลาที่เย่เดินไปตามถนนบางลา ช่างเป็นบรรยากาศที่บ้าคลั่งและไม่ได้เป็นสถานที่ที่จะพาลูก ๆ ของคุณมาด้วยแม้ในช่วงวันหยุดตอนกลางคืน",
        },
        {
          Review:
            "Wondrerful white sandy beach.  Many beach clubs with amenities - pools, food, drinks poolside or seated in pools, showers and toilet facilities.  Water from Andaman Sea is calm and nice to float in!  Skidoos and kite sailing available.  Everything for beach lovers like me!",
          Name: "Jim D",
          Address: "Ulaanbaatar, mongolia",
          Time: "Date of experience: January 2020",
          Rating: 4,
          Thai:
            "หาดทรายสีขาวมหัศจรรย์ คลับริมหาดหลายแห่งที่มีสิ่งอำนวยความสะดวกเช่นสระว่ายน้ำอาหารเครื่องดื่มริมสระน้ำหรือนั่งในสระน้ำฝักบัวและสิ่งอำนวยความสะดวกในห้องน้ำ น้ำจากทะเลอันดามันนั้นสงบและดีที่จะล่องลอยใน skidoos และการเล่นว่าว ทุกอย่างสำหรับคนรักชายหาดอย่างฉัน",
        },
        {
          Review:
            "We decided to spend Christmas Day 2019 at Patong Beach as we had been planning since early October! The beach was fairly crowded and the water is a bit dirty (in comparison to other Thai beaches) but overall it was a nice experience. We found some space among the people…",
          Name: "Michael",
          Address: "Woking, United Kingdom",
          Time: "Date of experience: December 2019",
          Rating: 3,
          Thai:
            "เราตัดสินใจที่จะใช้วันคริสต์มาสสองพันสิบเก้าที่หาดป่าตองเนื่องจากเราวางแผนมาตั้งแต่ต้นเดือนตุลาคมชายหาดค่อนข้างแออัดและน้ำค่อนข้างสกปรกเมื่อเทียบกับชายหาดไทยอื่น ๆ แต่โดยรวมแล้วมันเป็นประสบการณ์ที่ดี เราพบที่ว่างในหมู่คน",
        },
        {
          Review:
            "The Patong Beach is very well maintained. Beach and water are fairly clean, with many water activities to do. Swimmers are separated from all the other activities so you can enjoy your swim in peace. There are a lots of restaurants, bars and cafes along the beach, as well as…",
          Name: "Samir A",
          Address: "Ryde, Australia",
          Time: "Date of experience: January 2020",
          Rating: 5,
          Thai:
            "หาดป่าตองได้รับการดูแลอย่างดี ชายหาดและน้ำค่อนข้างสะอาดมีกิจกรรมทางน้ำมากมายให้ทำ นักว่ายน้ำแยกออกจากกิจกรรมอื่น ๆ ทั้งหมดเพื่อให้คุณสามารถเพลิดเพลินกับการว่ายน้ำอย่างสงบ มีร้านอาหารบาร์และร้านกาแฟมากมายตามชายหาดรวมทั้ง",
        },
        {
          Review:
            "We was staying in Patong for three weeks and went to the beach most days  It is a long beach if you walk from one ent to the other Can be a bit busy John",
          Name: "john q",
          Address: "Bolton, Greater Manchester",
          Time: "Date of experience: December 2019",
          Rating: 4,
          Thai:
            "เราพักในป่าตองเป็นเวลาสามสัปดาห์และไปที่ชายหาดเกือบทุกวันมันเป็นหาดยาวถ้าคุณเดินจากที่หนึ่งไปที่อื่น ๆ อาจจะค่อนข้างยุ่งจอห์น",
        },
        {
          Review:
            "Beach gets very busy but if you get there early enough to watch the sunrise it's amazing and peaceful. We also walked on the beach every night, it's very safe with lots of other people walking on the beach.",
          Name: "Therusha15",
          Address: "Johannesburg, South Africa",
          Time: "Date of experience: January 2020",
          Rating: 4,
          Thai:
            "ชายหาดจะยุ่งมาก แต่ถ้าคุณไปถึงที่นั่นเร็วพอที่จะดูพระอาทิตย์ขึ้นมันน่าอัศจรรย์และเงียบสงบ เรายังเดินบนชายหาดทุกคืนมันปลอดภัยมากมีผู้คนมากมายที่เดินบนชายหาด",
        },
        {
          Review:
            "Very nice beach. Great place for families. Children can have great fun. Very safe and secure. All kinds of rides available. Para sailing, jet ski’s, banana boats and all. Lots of good eating places in vicinity.",
          Name: "Kamal S",
          Address: "-",
          Time: "Date of experience: January 2020",
          Rating: 5,
          Thai:
            "ชายหาดที่ดีมาก สถานที่ที่เหมาะสำหรับครอบครัว เด็ก ๆ สามารถมีความสุขได้ ปลอดภัยมากและปลอดภัย มีเครื่องเล่นทุกชนิด แล่นเรือใบเจ็ทสกีเรือกล้วยและอื่น ๆ สถานที่รับประทานอาหารที่ดีมากมายในบริเวณใกล้เคียง",
        },
        {
          Review:
            "Comparing to other beaches in Thailand this is not by far the best beach. It has severall water sports available, like jet ski, parasailing, banana towed by speed boat. It has umbrellas with chairs for renting by 200 Baht per dy.",
          Name: "agnusporfius",
          Address: "Lisbon, Portugal",
          Time: "Date of experience: December 2019",
          Rating: 3,
          Thai:
            "เมื่อเปรียบเทียบกับชายหาดอื่น ๆ ในประเทศไทยนี่ไม่ใช่ชายหาดที่ดีที่สุด มันมีกีฬาทางน้ำที่ใช้ได้ทั้งหมดเช่นเจ็ทสกีพาราเซลลิงกล้วยลากโดยเรือเร็ว มีร่มพร้อมเก้าอี้ให้เช่าสองร้อยบาทต่อห้อง",
        },
        {
          Review:
            "We really enjoyed swimming & relaxing on the Patong beach, it was just 5min walk to our hotel. there is so much to do here, swimming, jet skii, parasailing. My daughter really enjoyed it here. while in the beach, dont forget to enjoy their pancakes & make your own icecream with…",
          Name: "ekm1masia",
          Address: "-",
          Time: "Date of experience: December 2019",
          Rating: 5,
          Thai:
            "เรามีความสุขกับการว่ายน้ำ & พักผ่อนบนชายหาดป่าตองเพียง 5 นาทีก็ถึงโรงแรมของเรา มีหลายอย่างให้ทำที่นี่ว่ายน้ำเจ็ตสกีพาราเซลลิ่ง ลูกสาวของฉันมีความสุขที่นี่จริง ๆ ในขณะที่อยู่บนชายหาดอย่าลืมเพลิดเพลินกับแพนเค้กและทำไอศครีมของคุณเองด้วย",
        },
        {
          Review:
            "it can get a bit crowded, busy and noisy, but it is a very good place to watch the sunset, but it is a very convenient beach with a lot of shops and restaurants, not so perfect for couples who look for romantic holidays but perfect for family.",
          Name: "KYS",
          Address: "-",
          Time: "Date of experience: December 2019",
          Rating: 4,
          Thai:
            "มันสามารถรับได้ค่อนข้างแออัดวุ่นวายและมีเสียงดัง แต่มันเป็นสถานที่ที่ดีมากในการชมพระอาทิตย์ตก แต่มันเป็นชายหาดที่สะดวกมากมีร้านค้าและร้านอาหารมากมายไม่เหมาะสำหรับคู่รักที่มองหาวันหยุดแสนโรแมนติก แต่สมบูรณ์แบบ สำหรับครอบครัว",
        },
        {
          Review:
            "Thailand has some of the most beautiful beaches in the world and Patong beach is one of them. Offering different kinds of water sports and a sea as warm as a bath. Plenty of beach sellers selling anything from cold drinks to sunglasses. The seller's are very nice and if you…",
          Name: "michael k",
          Address: "Sheffield, United Kingdom",
          Time: "Date of experience: January 2020",
          Rating: 5,
          Thai:
            "ประเทศไทยมีชายหาดที่สวยที่สุดในโลกและหาดป่าตองเป็นหนึ่งในนั้น นำเสนอกีฬาทางน้ำประเภทต่างๆและทะเลที่อบอุ่นราวกับอ่างอาบน้ำ ผู้ขายริมหาดมากมายที่ขายของทุกอย่างตั้งแต่เครื่องดื่มเย็นไปจนถึงแว่นกันแดด ผู้ขายเป็นคนดีมากและถ้าคุณ",
        },
        {
          Review:
            "USA resident and international traveler here: I was not at all impressed with Patong. Save yourself a trip and go to the Mexican Riviera Maya instead. The beach was dirty, the streets stink, and the hustlers on and around the beach are overwhelming. Everyone said this place…",
          Name: "Erich",
          Address: "San Diego, California",
          Time: "Date of experience: January 2020",
          Rating: 2,
          Thai:
            "ที่อาศัยอยู่ในสหรัฐอเมริกาและนักท่องเที่ยวต่างชาติที่นี่ฉันไม่ประทับใจเลยกับป่าตอง บันทึกการเดินทางของคุณและไปที่มายาริเวียร่ามายาแทน ชายหาดสกปรกถนนมีกลิ่นเหม็นและนักธุรกิจที่เดินทอดน่องไปรอบ ๆ ทุกคนพูดที่นี่",
        },
        {
          Review:
            "Stayed at Blue Ocean Resort. Easy walk to Patong beach passing many restaurants, bars & shops..  Longboat rides, jet skis & parachuting or just lazing on the beach. Plenty of opportunities to book a variety of trips to other islands or places of interest.",
          Name: "Jacmur2015",
          Address: "New Milton, United Kingdom",
          Time: "Date of experience: January 2020",
          Rating: 5,
          Thai:
            "พักที่บลูโอเชี่ยนรีสอร์ท เดินไปหาดป่าตองได้ง่ายผ่านร้านอาหารบาร์และร้านค้ามากมาย ขี่เรือยาวเจ็ทสกีและกระโดดร่มหรือแค่พักผ่อนบนชายหาด โอกาสมากมายที่จะจองทริปที่หลากหลายไปยังเกาะอื่น ๆ หรือสถานที่น่าสนใจ",
        },
        {
          Review:
            "Dirty looking water beach attractions that seemed a total rip off mainly parachute crack.. after watching I timed the air time and a disgusting 1 minute 20 seconds for something like 2000 baht",
          Name: "simon b",
          Address: "Barrow-in-Furness, United Kingdom",
          Time: "Date of experience: January 2020",
          Rating: 2,
          Thai:
            "สถานที่ท่องเที่ยวทางน้ำสกปรกมองชายหาดที่ดูเหมือนจะฉีกออกทั้งหมดส่วนใหญ่แตกร่มชูชีพ หลังจากดูฉันหมดเวลาออกอากาศและน่าขยะแขยงหนึ่งนาทียี่สิบวินาทีสำหรับบางอย่างเช่นสองพันบาท",
        },
        {
          Review:
            "Beautiful white sand beach, a little crowded and noisy in high season. Amazing water, warm and clean I recommend fresh fruit juices sold by merchants near the beach.. are excellent",
          Name: "Maria Doiciu",
          Address: "-",
          Time: "Date of experience: December 2019",
          Rating: 4,
          Thai:
            "หาดทรายขาวสวยงามมีผู้คนพลุกพล่านและมีเสียงดังในฤดูท่องเที่ยว น้ำที่น่าตื่นตาตื่นใจอบอุ่นและสะอาดฉันแนะนำน้ำผลไม้สดขายโดยพ่อค้าใกล้ชายหาด ยอดเยี่ยมมาก",
        },
        {
          Review:
            "One of the most spectacular beaches of Asia drawing tourists from around the world and filled with activity. The beach is clean and lined with a wide variety of bars and eateries providing seafood and other food for lunch and dinner. Weather is pleasant during Winter months and…",
          Name: "funnytrotter",
          Address: "-",
          Time: "Date of experience: December 2019",
          Rating: 5,
          Thai:
            "หนึ่งในชายหาดที่งดงามที่สุดของเอเชียดึงดูดนักท่องเที่ยวจากทั่วโลกและเต็มไปด้วยกิจกรรม ชายหาดสะอาดและเรียงรายไปด้วยบาร์และร้านอาหารมากมายที่ให้บริการอาหารทะเลและอาหารอื่น ๆ สำหรับมื้อกลางวันและมื้อค่ำ อากาศสบายในช่วงฤดูหนาวและเดือน",
        },
        {
          Review:
            "The Northern end (near Gracelands)  is nicer, with less people and cleaner water. For a couple hundred baht you can get a sun lounge under an umbrella for the day. Drinks are there and food carts. The security guys at Gracelands help you to navigate the road crossing. There's…",
          Name: "Itsjustfood",
          Address: "-",
          Time: "Date of experience: January 2020",
          Rating: 4,
          Thai:
            "ตอนเหนือสุดใกล้กับ gracelands คือ nicer มีคนน้อยและน้ำสะอาด สำหรับสองสามร้อยบาทคุณสามารถอาบแดดใต้ร่มสำหรับวัน เครื่องดื่มและรถเข็นอาหาร เจ้าหน้าที่รักษาความปลอดภัยที่เกรซแลนด์ช่วยคุณนำทางข้ามถนน มี",
        },
        {
          Review:
            "We went there on the 01/01/2020. Crowded but lots of activities. My granddaughter enjoyed herself. Sure will visit.again",
          Name: "Josephine J",
          Address: "Singapore, Singapore",
          Time: "Date of experience: December 2019",
          Rating: 4,
          Thai:
            "เราไปที่นั่นเมื่อวันที่ 01/01/2020 แออัด แต่มีกิจกรรมมากมาย หลานสาวของฉันมีความสุขกับตัวเอง แน่นอนว่าจะไป อีกครั้ง",
        },
        {
          Review:
            "A lot of people, famous walking street - Bangla road is here. But if you come with children recommender find more quiet place for vacation.",
          Name: "Emma Baker",
          Address: "Budapest, Hungary",
          Time: "Date of experience: December 2019",
          Rating: 4,
          Thai:
            "ผู้คนมากมายถนนคนเดินที่มีชื่อเสียงถนนบางลาอยู่ที่นี่ แต่ถ้าคุณมากับเด็ก ๆ ผู้แนะนำจะพบกับสถานที่ที่เงียบสงบกว่าสำหรับวันหยุดพักผ่อน",
        },
        {
          Review:
            "This beach probably is the worst in Phuket. Too many people, garbage left everywhere, very little swimming area, dirty water because most of it is taken by the watercraft and boats. Noisy because too close to the main road. Don't expect to lay down in paradise -it's not!",
          Name: "Andrey M",
          Address: "-",
          Time: "Date of experience: January 2020",
          Rating: 2,
          Thai:
            "ชายหาดนี้น่าจะเลวร้ายที่สุดในภูเก็ต มีคนจำนวนมากขยะทิ้งไปทุกที่บริเวณสระว่ายน้ำน้อยมากน้ำสกปรกเพราะส่วนใหญ่เป็นเรือและเรือ เสียงดังเพราะใกล้ถนนใหญ่เกินไป อย่าคาดหวังว่าจะนอนลงบนสวรรค์ไม่ได้",
        },
        {
          Review:
            "This beach is not the best in phuket. There are many beaches better and more clean to visit during your stay. It is location is amazing. Near patong market. I went to it only once during my stay.",
          Name: "Nadine E",
          Address: "Cairo, Egypt",
          Time: "Date of experience: January 2020",
          Rating: 3,
          Thai:
            "ชายหาดนี้ไม่ดีที่สุดในภูเก็ต มีชายหาดหลายแห่งที่ดีกว่าและสะอาดกว่าให้เยี่ยมชมระหว่างการพักของคุณ มันเป็นสถานที่ที่น่าตื่นตาตื่นใจ ใกล้ตลาดป่าตอง ฉันไปที่นั่นครั้งเดียวระหว่างที่ฉันพัก",
        },
        {
          Review:
            "My husband, our 10 years old son and I went to Patong beach. My son like the beach so much. As u walk pass by, there will be locals promoting jetski & parachuting. They a bit quite pushy, we politely reject them as we are not interested, they keep mumbling non-stop. They are very rude & not friendly. Phuket is not a friendly spot. If can, try to avoid this place. Otherwise your holidays gonna be spoiled by their sh*t attitude",
          Name: "Ms Chongg",
          Address: "Malaysia",
          Time: "Date of experience: January 2020",
          Rating: 1,
          Thai:
            "สามีของฉันลูกชายอายุสิบขวบของฉันและฉันไปที่หาดป่าตอง ลูกชายของฉันชอบชายหาดมาก ขณะที่คุณเดินผ่านจะมีชาวบ้านที่ส่งเสริม jetski และกระโดดร่ม พวกเขาค่อนข้างเร่งเร้าเราปฏิเสธพวกเขาอย่างสุภาพในขณะที่เราไม่สนใจพวกเขาพูดพึมพำไม่หยุดยั้ง พวกเขาหยาบคายมากและไม่เป็นมิตร ภูเก็ตไม่ใช่สถานที่ที่เป็นมิตร ถ้าทำได้ให้พยายามหลีกเลี่ยงสถานที่นี้ มิฉะนั้นวันหยุดของคุณจะถูกทำลายโดยทัศนคติ sh * t ของพวกเขา",
        },
        {
          Review:
            "Loungers and umberella cost 100 baths. They make sure there is no sand on lounger and place your towel on it Towels can be rented if needed. Plenty of women coming round to see if you want a drink or fresh fruit, all reasonably priced. Sea quite calm no big waves",
          Name: "Christine B",
          Address: "Cheadle, United Kingdom",
          Time: "Date of experience: January 2020",
          Rating: 5,
          Thai:
            "เก้าอี้และเออเบลล่าราคาหนึ่งร้อยบาท พวกเขาทำให้แน่ใจว่าไม่มีทรายบนเก้าอี้และวางผ้าเช็ดตัวของคุณบนมันสามารถเช่าผ้าเช็ดตัวถ้าจำเป็น ผู้หญิงจำนวนมากมารอบเพื่อดูว่าคุณต้องการเครื่องดื่มหรือผลไม้สดราคาสมเหตุสมผลทั้งหมด ทะเลค่อนข้างสงบไม่มีคลื่นลูกใหญ่",
        },
        {
          Review:
            "All hotels are off the beach and that is ok. Make sure you get to the beach early to get a lounge chair. Reserve one with Alex the charge for 2 chairs and an umbrella is 200 Bhats. If you reserve for the next day it costs you 270 Bhats but you get preferential treatment and an extra umbrella. Eat the food off the carts on the beach it is amazingly good. Find If the ice cream guy he is very knowledgeable and can speak good English. Massages are better and less expensive off the beach. The water is amazing and the sun is very strong. I did not spend time in the sun and came back with a nice tan. Don’t bring too many clothes as laundry services are available everywhere for 50 Bhats per kilo. You can change money almost anywhere and the people are amazing. There are more 711 stores in Patong beach than in CANADA every street corner has at least one. Pharmacies are also everywhere. Eat street food at the night markets it is amazing. Have fun bring sun screen. Be careful crossing the streets as the experience is like dodging bulls. Russian roulette.",
          Name: "Ron S",
          Address: "Okotoks, Canada",
          Time: "Date of experience: January 2020",
          Rating: 5,
          Thai:
            "โรงแรมทั้งหมดอยู่นอกชายหาดและก็ใช้ได้ ให้แน่ใจว่าคุณไปที่ชายหาดก่อนเพื่อรับเก้าอี้เลานจ์ จองหนึ่งกับ alex ค่าธรรมเนียมสำหรับเก้าอี้สองตัวและร่มสองร้อย bhats หากคุณจองในวันถัดไปคุณจะต้องเสียค่าใช้จ่ายสองร้อยเจ็ดสิบ bhats แต่คุณจะได้รับสิทธิพิเศษและร่มพิเศษ กินอาหารนอกรถเข็นบนชายหาดมันเป็นสิ่งที่ดีอย่างน่าอัศจรรย์ ค้นหาว่าคนที่แต่งตัวประหลาดไอศครีมเขามีความรู้มากและสามารถพูดภาษาอังกฤษได้ดี การนวดจะดีกว่าและราคาไม่แพงจากชายหาด น้ำนั้นวิเศษมากและแสงอาทิตย์ก็แรงมาก ฉันไม่ได้ใช้เวลาในดวงอาทิตย์และกลับมาพร้อมกับผิวสีแทนสวย อย่านำเสื้อผ้ามากเกินไปเพราะมีบริการซักรีดทุกห้าสิบบาทต่อกิโลกรัม คุณสามารถเปลี่ยนเงินได้เกือบทุกที่และผู้คนน่าทึ่ง มีร้านค้าเจ็ดร้อยสิบเอ็ดร้านในหาดป่าตองกว่าในแคนาดาทุกมุมถนนมีร้านอย่างน้อยหนึ่งร้าน ร้านขายยาก็มีทุกที่ กินอาหารข้างทางที่ตลาดโต้รุ่งมันวิเศษมาก มีความสนุกสนานนำหน้าจอดวงอาทิตย์ ระวังการข้ามถนนเพราะประสบการณ์เป็นเหมือนการหลบฝูงวัว รูเล็ตรัสเซีย",
        },
        {
          Review:
            "Been to Thailand Bangkok, Phuket and Phi Phi Islands, but i would vouch for my days at Phuket, they were so awesome. the Place is so welcoming and so full of life, a lot of activities around the beach. and the waters are warm and so blue. if i am to come back to Thailand, all my days would be spent in Phuket along Patong Beach.",
          Name: "Paycheal S",
          Address: "Gaborone, Botswana",
          Time: "Date of experience: December 2019",
          Rating: 5,
          Thai:
            "เคยไปกรุงเทพประเทศไทยเกาะภูเก็ตและเกาะพีพี แต่ฉันจะรับรองวันเวลาของฉันที่ภูเก็ตพวกเขายอดเยี่ยมมาก เป็นสถานที่ที่ให้การต้อนรับและเต็มไปด้วยชีวิตกิจกรรมมากมายรอบ ๆ ชายหาด และน้ำก็อุ่นและน้ำเงิน ถ้าฉันจะกลับมาเมืองไทยทุกวันของฉันจะถูกใช้ในภูเก็ตตามชายหาดป่าตอง",
        },
        {
          Review:
            "Lovely clean beach with various things to do. Massages on the beach, jet skis and more. Close to the hotel and stunning views.",
          Name: "srfrankland",
          Address: "Auckland, New Zealand",
          Time: "Date of experience: January 2020",
          Rating: 4,
          Thai:
            "ชายหาดที่น่ารักสะอาดมีกิจกรรมน่าสนใจมากมาย การนวดบนชายหาดเจ็ทสกีและอื่น ๆ ใกล้กับโรงแรมและวิวที่สวยงาม",
        },
        {
          Review:
            "Great beach on Phuket. The town is a dump. They have roped areas for swimming. Chair and umbrella rentals are available for 200 Baht.",
          Name: "lazytraveller13",
          Address: "Toronto, Canada",
          Time: "Date of experience: January 2020",
          Rating: 5,
          Thai:
            "ชายหาดที่ดีในจังหวัดภูเก็ต เมืองนี้เป็นกองขยะ พวกเขามีพื้นที่เชือกสำหรับว่ายน้ำ เก้าอี้และร่มให้เช่าสองร้อยบาท",
        },
        {
          Review:
            "This is not my kind of place at all. Too many bodies, chairs, beds, umbrellas all on top of each other. There is no personal space. It probably isn’t, but it feels dirty. Hated it.",
          Name: "SteffiSpain",
          Address: "Utorda, India",
          Time: "Date of experience: January 2020",
          Rating: 1,
          Thai:
            "นี่ไม่ใช่สถานที่ของฉันเลย ร่างกาย, เก้าอี้, เตียง, ร่มมากเกินไป ไม่มีพื้นที่ส่วนตัว มันอาจจะไม่ใช่ แต่รู้สึกสกปรก เกลียดมัน",
        },
        {
          Review:
            "Clean beach Too many people though and a lot of touting by people selling stuff. It’s annoying when you’re having a conversation with someone or enjoying a quiet moment staring into the sea and sunset with a beer.It’s worth a visit because it’s conveniently located beside Bangla street. Nice sun set but couldn’t see it setting over the horizon.Popular common Beach",
          Name: "londonchoco",
          Address: "Singapore, Singapore",
          Time: "Date of experience: December 2019",
          Rating: 3,
          Thai:
            "ชายหาดสะอาดเกินไปผู้คนมากมายแม้ว่าจะมีคนขายสิ่งของเยอะ มันน่ารำคาญเมื่อคุณกำลังสนทนากับใครบางคนหรือเพลิดเพลินกับช่วงเวลาที่เงียบสงบจ้องมองทะเลและพระอาทิตย์ตกด้วยเบียร์ มันคุ้มค่าแก่การมาเยี่ยมชมเพราะตั้งอยู่ข้างถนนบางลา พระอาทิตย์ตกที่สวยงาม แต่ไม่สามารถมองเห็นมันได้เหนือขอบฟ้า ชายหาดยอดนิยมทั่วไป",
        },
        {
          Review:
            "The beach is generally clean with enough swimming space and planty of activities to do. It is also close to the shopping centers and restaurants. The loungers are reasonably priced.",
          Name: "Quinton M",
          Address: "Johannesburg, South Africa",
          Time: "Date of experience: January 2020",
          Rating: 4,
          Thai:
            "ชายหาดโดยทั่วไปสะอาดมีพื้นที่เล่นน้ำเพียงพอและมีกิจกรรมให้ทำมากมาย นอกจากนี้ยังใกล้กับศูนย์การค้าและร้านอาหาร เก้าอี้มีราคาสมเหตุสมผล",
        },
        {
          Review:
            "This beach has everything exactly where you need it. The people at the restaurants are super friendly. You have the options of umbrellas and chairs to enjoy some much needed shade. It is a great beach to swim at or try out some adventure sports. I personally enjoyed watching the gorgeous sunsets. It is really peaceful. If you looking for somewhere to see the New Year in, this is a great spot. If you have never been, check it out!",
          Name: "Lisa v",
          Address: "Hong Kong, China",
          Time: "Date of experience: January 2020",
          Rating: 5,
          Thai:
            "ชายหาดนี้มีทุกสิ่งที่คุณต้องการ ผู้คนที่ร้านอาหารเป็นกันเองสุด ๆ คุณมีตัวเลือกของร่มและเก้าอี้ที่จะเพลิดเพลินไปกับร่มเงาที่จำเป็นมาก มันเป็นชายหาดที่ดีในการว่ายน้ำหรือลองเล่นกีฬาผจญภัย ฉันสนุกกับการดูพระอาทิตย์ตกที่สวยงาม มันสงบจริงๆ หากคุณกำลังมองหาสถานที่เพื่อดูปีใหม่นี้เป็นจุดที่ดีมาก ถ้าคุณยังไม่เคยไปให้ลองดู",
        },
        {
          Review:
            "It was our second stay there. Very nice place for swimming and sunbathing. Excelent service whole day, many offers from local sellers for many of local products or drinks. Behind the beach are many of streetpoints for local of Thai food.",
          Name: "milankov",
          Address: "Banska Bystrica, Slovakia",
          Time: "Date of experience: January 2020",
          Rating: 5,
          Thai:
            "มันเป็นการพักครั้งที่สองของเราที่นั่น เป็นสถานที่ที่ดีมากสำหรับการว่ายน้ำและอาบแดด บริการที่ยอดเยี่ยมตลอดทั้งวันข้อเสนอมากมายจากผู้ขายในท้องถิ่นสำหรับผลิตภัณฑ์หรือเครื่องดื่มในท้องถิ่นมากมาย ด้านหลังชายหาดมีจุดที่น่าสนใจมากมายสำหรับอาหารท้องถิ่น",
        },
      ],
      fields: [
        {
          key: "Review",
          label: "Review",
          sortable: true,
          sortDirection: "desc",
        },
        {
          key: "Rating",
          label: "Rating",
          sortable: true,
          class: "text-center",
        },
      ],
      totalRows: 3,
      currentPage: null,
      perPage: 5,
      pageOptions: [5, 10, 50],
      sortBy: "",
      sortDesc: false,
      sortDirection: "asc",
      filter: null,
      filterOn: [],
      infoModal: {
        id: "info-modal",
        title: "",
        content: "",
      },
    };
  },
  computed: {
    sortOptions() {
      // Create an options list from our fields
      return this.fields
        .filter((f) => f.sortable)
        .map((f) => {
          return { text: f.label, value: f.key };
        });
    },
  },
  mounted() {
    // Set the initial number of items
    this.totalRows = this.item.length;
  },
  methods: {
    info(item, index, button) {
      this.infoModal.title = `Row index: ${index}`;
      this.infoModal.content = JSON.stringify(this.item, null, 2);
      this.$root.$emit("bv::show::modal", this.infoModal.id, button);
    },
    resetInfoModal() {
      this.infoModal.title = "";
      this.infoModal.content = "";
    },
    onFiltered(filteredItems) {
      // Trigger pagination to update the number of buttons/pages due to filtering
      this.totalRows = filteredItems.length;
      this.currentPage = 1;
    },
  },
};
</script>

<style scoped>
#space {
  margin-bottom: 40px;
}

</style>