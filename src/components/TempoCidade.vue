<script>
export default {
  props: {
    cidade: {
      type: Object,
      required: true,
    },
    bandeira: {
      type: String,
      required: true,
    },
  },
};
</script>

<template>
  <div class="flex justify-center">
    <div class="w-96 bg-white rounded-lg shadow-lg p-6 m-4">
      <!-- create a header -->
      <div class="flex justify-between items-center">
        <h1 class="text-2xl font-bold">
          {{ cidade.location.name }} /
          {{ cidade.location.region }}
        </h1>
        <h1>{{ cidade.current.temp_c }}ºC</h1>
        <img :src="cidade.current.condition.icon" />
      </div>
      <div class="mt-8">
        <h1>Sensação térmica: {{ cidade.current.feelslike_c }}ºC</h1>
        <h1>Umidade: {{ cidade.current.humidity }}%</h1>
        <h1>Velocidade do vento: {{ cidade.current.wind_kph }}km/h</h1>
        <h1>Porcentagem de nuvens no céu: {{ cidade.current.cloud }}%</h1>
        <h1>
          Fuso-Horário: {{ cidade.location.tz_id }} \\
          {{ cidade.location.localtime }}
        </h1>

        <code class="bg-blend-darken bg-gray-700 text-white text-xs p-1">
          Latitude: {{ cidade.location.lat }}/Longitude:
          {{ cidade.location.lon }}</code
        >
        <div class="max-w flex justify-center mt-2">
          <img :src="bandeira" />
        </div>
      </div>
    </div>
  </div>
</template>
