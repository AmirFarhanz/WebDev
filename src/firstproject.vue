<script setup>

import { ref, onMounted } from "vue";
let prayerTime = ref([])

onMounted(async function () {
  
  let response = await fetch('https://www.e-solat.gov.my/index.php?r=esolatApi/TakwimSolat&period=today&zone=WLY01')
  let data = await response.json()
  prayerTime.value = data.prayerTime
  
})

</script>

<template>
  <div v-for="time in prayerTime">
 <table class="border-solid border-2 border-sky-500">
  <thead>
    <tr>
    <th>hijri</th>
    <th>date</th>
    <th>day</th>
    <th>Imsak</th>
    <th>Fajr</th>
    <th>Syuruk</th>
    <th>Dhuhr</th>
    <th>Asr</th>
    <th>Maghrib</th>
    <th>Isyak</th>
    </tr>
    
  </thead>
  <tbody>
    <tr>
      <td>{{ time.hijri }}</td>
    <td>{{ time.date }}</td>
    <td>{{ time.day }}</td>
    <td>{{ time.imsak }}</td>
    <td>{{ time.fajr }}</td>
    <td>{{ time.syuruk }}</td>
    <td>{{ time.dhuhr }}</td>
    <td>{{ time.asr }}</td>
    <td>{{ time.maghrib }}</td>
    <td>{{ time.isha }}</td>
    </tr>
    
  </tbody>
 </table>
  </div>

</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
