<template>
  <div class="flex flex-col mt-10 items-center">
    <div class="flex mx-14 mb-2">
      <button @click="downloadPDF" class="py-1 px-3 rounded-md flex flex-row text-white bg-red-600">
        <div><BxSolidDownload class="text-2xl text-white" /></div>
        <div class="text-white">Download</div>
      </button>
    </div>
    <section ref="contentToDownload" class="flex flex-col items-center mx-16 p-5">
      <div>Hello, your Text or custom page which will export or download</div>
    </section>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { BxSolidDownload } from '@kalimahapps/vue-icons'
import { jsPDF } from 'jspdf'
import html2canvas from 'html2canvas'

// Download function
const contentToDownload = ref(null)
const downloadPDF = async () => {
  if (contentToDownload.value) {
    const canvas = await html2canvas(contentToDownload.value)
    const imgData = canvas.toDataURL('image/png')

    const pdf = new jsPDF()

    pdf.addImage(imgData, 'SVG', 10, 10, 190, 0)

    // Save the PDF
    pdf.save('download.pdf')
  }
}
</script>

<style scoped>
/* Add any scoped styles if needed */
</style>
