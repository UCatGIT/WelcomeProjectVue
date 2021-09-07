<template>
  <div id="app">
    {{ title }}
    
  <div class="site-title">
    <h1>Welcome to Opportunity</h1>
    <span class="site-description">Dienstag {{currentDate}}</span>

      <div>
        
        
      </div>

  </div>
    <main>
      <div class="ersterAbschnitt"> 
       <ul class="entry-list"> 
         <li v-for="entry in filteredEntries" :key="entry.id" class="entry-item">
           <span class="entry-daytime">{{entry[0] }} Uhr, {{ entry[1].replaceAll("/", ".")}}</span>
           <br>
           <h3 class="entry-title">Opportunity Zürich</h3>
            <span class="entry-description">Trainees & Team will return from their Weekend</span>
         <br>
         </li>
         <li class="entry-item">
           <span class="entry-daytime">08:30 Uhr, 07.09.2021</span>
           <br>
           <h3 class="entry-title">Tugce Nur returns to the office</h3>
            <span class="entry-description">We will continue working on this app together on Tuesday!</span>
         <br>
         </li>
         <li class="entry-item">
           <span class="entry-daytime">15:00 Uhr, 08.09.2021</span>
           <br>
           <h3 class="entry-title">Firmenausflug Panter</h3>
            <span class="entry-description">Opportunity goes to Limmatplatz and visits the web agnecy Panter</span>
         <br>
         </li>
       </ul>
      </div>
    </main>


    <footer>
      <div> <img src="./assets/STZH_SEB_Logo.png" alt="Logo1" width="230px" height="44px"></div>
      <div> <img src="./assets/Opportunity.png" alt="Logo2" width="296px" height="55px"></div>
      <div><img src="./assets/SAG_Logo_De.png" alt="Logo2" width="273px" height="52px"></div>
    </footer>
   


  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'App',
  data() {
    return {
      title: "Welcome screen Urs",
      currentDate: "",
      gsheet_url: "https://sheets.googleapis.com/v4/spreadsheets/1qLZJwuNv3QmwGhSj1wZZbuXNOkDKN-Ha7fo0Ca_uVVU/values:batchGet?ranges=A1%3AE100&valueRenderOption=FORMATTED_VALUE&key=AIzaSyBesotaNgSaTUIhrSKjEaExdi-ksKInhoE",
      entries: [],
    };
  },
  computed: {
    filteredEntries() {
      return[...this.entries].slice(1);
    },
  
  },
  methods: {
    getData() {
      axios.get(this.gsheet_url).then((response) => {
        this.entries =response.data
console.log(response);

      })
    },
    updateCurrentDate() {
      let today =new Date();
      const date = `${today.getDate()}.${today.getMonth()+1}.${today.getFullYear()}`;
      this.currentDate = date;
    },
    refreshData() {
      this.getData();
      this.updateCurrentDate();
    },
  },
  mounted() {
    this.refreshData(); 
    setInterval(() => {
      this.refreshData();      
    }, 1800000);
  },
};



</script>



<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@500;900&display=swap');

body {
  background-color: #E5E5E5;
}

#app {
  font-family: "Inter", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

footer {
  background-color:#fff;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  box-sizing: border-box;
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  padding: 40px;
  color: chocolate;
}
footer div {
  flex-grow: 1;
}




.site-title {
  font-size: 62px;
  font-weight: 900;
  margin: 80px 0 20px 0;
}

h1 {
  font-size: 62px;
  font-weight: 900;
  margin: 80px 0 20px 0;
  color: #323d4a;
}

h3 {
  font-weight: 900;
  color: #ffbfab;
  
  
}

.site-description {
  color: #9aa7b1;
  font-size: 62px;
  font-weight: 500;
  margin: 0;

}




.entry-title {
  font-size: inherit;
}


.entry-list {
  text-align: left;
 
  color: #ffbfab;
}

.entry-daytime {
  color: #eb5e00;
  font-weight: 900;
  
}

.entry-item {
background-color: #0F05A0;
width: 80%;
padding: 35px 40px;
margin: 40px 0;
font-size: 28px;
line-height: 1.3;
list-style: none;
}


</style>
