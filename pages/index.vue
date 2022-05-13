<template>
  <div class="w-full h-screen container md:mx-auto md:px-6">
    <div class="flex flex-wrap lg:-mx-4 h-full">
      <div class="px-1 w-full md:w-1/2">
        <model-viewer
        :year="selectedYear"
        :enablePan="enablePan"
        :enableZoom="enableZoom"
        :enableRotate="enableRotate"
        :bgColor="selectedColor"
        :bgAlpha="bgAlpha" />
      </div>
      <div class="w-full md:w-1/2 md:p-12 px-12 py-4">
        <h3 class="text-2xl font-extrabold mb-4">
          GitHub Skyline <a class="text-red-500 italic underline" target="_blank" href="https://skyline.github.com/srestraj">@srestraj</a>
        </h3>

        <label for="options" class="mb-4 inline-block text-xl">Select Year to update model</label>

        <select id="options" v-model="selectedYear" class="form-select text-lg appearance-none block w-full md:w-1/2 px-3 py-1.5 text-base font-normal text-gray-700 bg-white border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none" aria-label="Default select example">
          <option v-for="year in years" :key="year.year" :value="year.year">
            {{ year.year }}
          </option>
        </select>

        <!-- controls -->
        <div class="controls w-full mt-5">
          <h3 class="text-xl mb-4">
            Controls
          </h3>
          <div class="mb-4">
            <button @click="toggle('pan')" class="inline-block mb-2 bg-transparent hover:bg-green-700 text-green-700 hover:text-white py-2 px-4 border border-green-500 hover:border-transparent rounded mx-auto">{{ enablePan ? 'Disable' : 'Enable' }} Translation</button>
            <button @click="toggle('zoom')" class="inline-block mb-2 bg-transparent hover:bg-green-700 text-green-700 hover:text-white py-2 px-4 border border-green-500 hover:border-transparent rounded mx-auto">{{ enableZoom ? 'Disable' : 'Enable' }} Zoom</button>
            <button @click="toggle('rotate')" class="inline-block mb-2 bg-transparent hover:bg-green-700 text-green-700 hover:text-white py-2 px-4 border border-green-500 hover:border-transparent rounded mx-auto">{{ enableRotate ? 'Disable' : 'Enable' }} Rotation</button>
          </div>

          <div>
            <label for="color" class="mb-4 inline-block text-lg">Select background color</label>
            <input id="color" v-model="selectedColor" type="color" class="bg-transparent border-transparent rounded" name="color">
          </div>

          <div>
            <label for="options" class="my-4 inline-block text-lg">Select alpha value</label>
            <select id="options" v-model="bgAlpha" class="form-select text-lg appearance-none block w-1/2 md:w-1/4 px-3 py-1.5 text-base font-normal text-gray-700 bg-white border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none" aria-label="Default select example">
              <option v-for="alphaValue in alphaOptions" :key="alphaValue.value" :value="alphaValue.value">
                {{ alphaValue.value }}
              </option>
            </select>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data () {
    return {
      selectedYear: '2019',
      selectedColor: '#13ce66',
      bgAlpha: 0.5,
      years: [
        {
          year: '2019',
          selected: true
        },
        {
          year: '2020',
          selected: false
        },
        {
          year: '2021',
          selected: false
        },
        {
          year: '2022',
          selected: false
        }
      ],
      alphaOptions: [
        {
          value: 0
        },
        {
          value: 0.5
        },
        {
          value: 1
        }
      ],
      enablePan: true,
      enableZoom: true,
      enableRotate: true
    }
  },
  methods: {
    toggle (type) {
      if (type === 'pan') {
        this.enablePan = !this.enablePan
      }
      if (type === 'zoom') {
        this.enableZoom = !this.enableZoom
      }
      if (type === 'rotate') {
        this.enableRotate = !this.enableRotate
      }
    }
  }
}
</script>
