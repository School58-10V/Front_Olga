<template>
  <div class= "test" :class="{ norender: this.kre === false }">
    <button class="zak" id="vakl" @click="vakl">X</button>
    <img src="../assets/Ins.png">
  </div>
  <div class="home">
    <img class="ek" :src="require(`../assets/Eb1_${yr}.png`)">
    <img :src="require(`../assets/Eb2_${yr}.png`)">
  </div>
  <div class="home">
    <img class="ek" :src="require(`../assets/Eb3_${yr}.png`)">
    <img src="../assets/Ms.png">
    <div1>
      <button @click="start()">Старт</button><br>
      <label>Количество светителей <input v-model="svetitels"></label><br>
      <label>Количество Жуков-Взрывателей <input v-model="beetles"></label><br>
      <label>Количество монстров в городе <input v-model="monsters"></label><br>
      <button @click="sendButton()" :class="{ norender: this.shr === false }">Отправить данные</button>
    </div1>
  </div>
</template>

<script>
    import axios from "axios";
    export default {
        components: {
        },
        data() {
                return {
                kre: true,
                shr: false,
                value: 1,
                svetitels: "",
                beetles: "",
                monsters: "",
                yr: "",
                p: 0,
                }
        },
        methods: {
            vakl() {
                    this.kre = false;
            },
            Timer() {
                if (this.p == 0 ) {
                    this.shr = false;
                    this.yr = "";
                    alert( "Плохо!" );
                }
            },
            start() {
                setTimeout(this.Timer, 30000);
                this.shr = true;
                axios.get("http://127.0.0.1:5000/api/v2/players").then(response => {
                this.yr = response.data[0].victories;
                })


            },
            sendButton() {
                this.shr = false;
                this.yr = "";
                let data = {
                    "svetitels": parseInt(this.svetitels),
                    "beetles": parseInt(this.beetles),
                    "monsters": parseInt(this.monsters),
                };
                console.log(data)
                if (data["svetitels"] == 6 && data["beetles"] == 7 && data["monsters"] == 4) {
                    this.p = 1;
                    alert( "Правильно!" );

                }

            }
        }
    }
</script>
<style scoped>
body {
  font-size: 4rem;
}
.home {
    padding-top: 2%;
}
button {
 font-family: Arial,Helvetica,sans-serif;
 font-size: 50px;
}
div1 {
    left: 58%;
    top: 60%;
    z-index: 5;
    position: fixed;
}
.ek {
    margin-right: 13%;
}
.test {
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    z-index: 5;
    position: fixed;
}
.zak {
    left: 93%;
    float: left;
    z-index: 3;
    position: absolute;
}
.norender {
  display: none;
}
</style>
