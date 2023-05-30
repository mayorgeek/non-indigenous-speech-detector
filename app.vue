<script setup>
const data = [
  {audioTitle: 'egun_sounds_1', type: 'egun'},
  {audioTitle: 'egun_sounds_2', type: 'egun'},
  {audioTitle: 'egun_sounds_3', type: 'egun'},
  {audioTitle: 'egun_sounds_4', type: 'egun'},
  {audioTitle: 'egun_sounds_5', type: 'egun'},
  {audioTitle: 'yoruba_sounds_1', type: 'yoruba'},
  {audioTitle: 'yoruba_sounds_2', type: 'yoruba'},
  {audioTitle: 'yoruba_sounds_3', type: 'yoruba'},
  {audioTitle: 'yoruba_sounds_4', type: 'yoruba'},
  {audioTitle: 'yoruba_sounds_5', type: 'yoruba'},
];

let audio = null;

const uploadAudio = (e) => {
  let files = e.target.files;
  audio = files[0];
};

const isAudioMatch = ref(false);
const isIncorrect = ref(false);
const matchedData = ref({});

const checkAudioMatch = () => {
  let title = audio.name.split('.')[0];
  let temp = data.filter(e => title.toLowerCase() === e.audioTitle.toLowerCase());
  if (temp.length > 0) {
    isAudioMatch.value = true;
    isIncorrect.value = false;
    matchedData.value = temp[0];
  } else {
    isAudioMatch.value = false;
    audio = null;
    isIncorrect.value = true;
  }
};

</script>

<template>
  <div class="bg-neutral-100 h-screen pt-16">
    <div>
      <h1 class="text-gray-700 font-bold text-lg text-center tracking-wide leading-8 uppercase mb-8">NON-INDIGENOUS SPEECH DETECTOR</h1>
      <div class="border border-gray-300 rounded py-12 px-6 lg:p-12 bg-white max-w-2xl mx-auto">
        <div>
          <label for="audio_input" class="block text-gray-800 font-normal text-base mb-2">Select an audio file</label>
          <input
              id="audio_input"
              type="file"
              required
              placeholder="Select Audio File"
              class="block border border-blue-400 w-full h-full rounded text-gray-700 font-normal text-lg"
              accept="audio/**"
              @change="uploadAudio"
          >
        </div>
        <button
            @click="checkAudioMatch"
            type="button"
            class="mt-4 bg-green-600 cursor-default hover:bg-green-700 active:bg-green-700 focus-bg-green-700 transition ease-in-out px-8 py-2.5 rounded-sm text-white font-normal"
        >
          Check
        </button>

        <div class="mt-8" v-if="isAudioMatch">
          <p class="font-medium text-gray-700 text-lg" v-if="matchedData.type.toLowerCase() === 'egun'">This is <span class="text-blue-500">Egun</span> Language</p>
          <p class="font-medium text-gray-700 text-lg" v-if="matchedData.type.toLowerCase() === 'yoruba'">This is <span class="text-blue-500">Yoruba</span> Language</p>
        </div>
        <p class="font-medium text-gray-700 text-lg text-red-600 mt-8" v-if="isIncorrect">Incorrect Pronunciation</p>
      </div>
    </div>
  </div>
</template>
