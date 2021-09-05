<template>
  <div>
    <div class="top-buttons">
      <button @click="makePdf">PDF</button>
      <!-- <button @click="loadImg">IMG</button> -->
    </div>
    <div class="pdf-container">
      <vue-html2pdf
        ref="html2Pdf"
        :show-layout="true"
        :float-layout="false"
        :enable-download="enableDownload"
        :preview-modal="false"
        :paginate-elements-by-height="1400"
        :filename="filename"
        :pdf-quality="2"
        :manual-pagination="true"
        pdf-format="a4"
        pdf-orientation="portrait"

        @progress="onProgress($event)"
        @hasStartedGeneration="hasStartedGeneration()"
        @hasGenerated="hasGenerated($event)"
        @beforeDownload="beforeDownload"
      >
        <section slot="pdf-content" class="pdf-content">
          <div :key="`card-${1}`" class="single-card">
            <img class="top-graphix" src="./stars.png" alt="stars.png">
            <div class="content">
              <div class="content-row">Datums: <div class="dashes" /></div>
              <div class="content-row">Svars: <div class="dashes" /></div>
              <div class="content-row">Augums: <div class="dashes" /></div>
              <div class="content-row">Galviņa: <div class="dashes" /></div>
              <div class="content-row">Krūtis: <div class="dashes" /></div>
              <div class="content-row">Nākošā vizīte: <div class="dashes" /></div>
              <div class="content-row">Ieteikumi: <div class="dashes" /></div>
              <div class="content-row"><div class="dashes" /></div>
              <div class="content-row"><div class="dashes" /></div>
              <div class="content-row"><div class="dashes" /></div>
            </div>
            <img class="bottom-graphix" src="./1.png">
          </div>
          <div :key="`card-${2}`" class="single-card">
            <img class="top-graphix" src="./stars.png" alt="stars.png">
            <div class="content">
              <div class="content-row">Datums: <div class="dashes" /></div>
              <div class="content-row">Svars: <div class="dashes" /></div>
              <div class="content-row">Augums: <div class="dashes" /></div>
              <div class="content-row">Galviņa: <div class="dashes" /></div>
              <div class="content-row">Krūtis: <div class="dashes" /></div>
              <div class="content-row">Nākošā vizīte: <div class="dashes" /></div>
              <div class="content-row">Ieteikumi: <div class="dashes" /></div>
              <div class="content-row"><div class="dashes" /></div>
              <div class="content-row"><div class="dashes" /></div>
              <div class="content-row"><div class="dashes" /></div>
            </div>
            <img class="bottom-graphix" src="./2.png">
          </div>
          <div :key="`card-${3}`" class="single-card">
            <img class="top-graphix" src="./stars.png" alt="stars.png">
            <div class="content">
              <div class="content-row">Datums: <div class="dashes" /></div>
              <div class="content-row">Svars: <div class="dashes" /></div>
              <div class="content-row">Augums: <div class="dashes" /></div>
              <div class="content-row">Galviņa: <div class="dashes" /></div>
              <div class="content-row">Krūtis: <div class="dashes" /></div>
              <div class="content-row">Nākošā vizīte: <div class="dashes" /></div>
              <div class="content-row">Ieteikumi: <div class="dashes" /></div>
              <div class="content-row"><div class="dashes" /></div>
              <div class="content-row"><div class="dashes" /></div>
              <div class="content-row"><div class="dashes" /></div>
            </div>
            <img class="bottom-graphix" src="./2.png">
          </div>
          <div :key="`card-${4}`" class="single-card">
            <img class="top-graphix" src="./stars.png" alt="stars.png">
            <div class="content">
              <div class="content-row">Datums: <div class="dashes" /></div>
              <div class="content-row">Svars: <div class="dashes" /></div>
              <div class="content-row">Augums: <div class="dashes" /></div>
              <div class="content-row">Galviņa: <div class="dashes" /></div>
              <div class="content-row">Krūtis: <div class="dashes" /></div>
              <div class="content-row">Nākošā vizīte: <div class="dashes" /></div>
              <div class="content-row">Ieteikumi: <div class="dashes" /></div>
              <div class="content-row"><div class="dashes" /></div>
              <div class="content-row"><div class="dashes" /></div>
              <div class="content-row"><div class="dashes" /></div>
            </div>
            <img class="bottom-graphix" src="./1.png">
          </div>
        </section>
      </vue-html2pdf>

    </div>
  </div>
</template>
<script>
import VueHtml2pdf from 'vue-html2pdf';

export default {
  name: 'App',
  components: { VueHtml2pdf  },
  data(){
    return {
      filename: `template`,
      enableDownload: false,
      pdf: true,
      img: ['../1.png', '../2.png', '../2.png', '../2.png'],
    };
  },
  methods: {
    // loadImg(){
    //   this.img[0] = './1.png';

    //   console.log(this.img);
    // },
    /** html2pdf events. */
    makePdf() {
      this.$refs.html2Pdf.generatePdf();
    },
    onProgress(){
      //
    },
    hasStartedGeneration(){
      //
    },
    hasGenerated(){
      //
    },
    async beforeDownload({ html2pdf, options, pdfContent }){
      if (this.pdf === true){
        console.log('%cDownload PDF', 'color: green;');
        html2pdf().set(options).from(pdfContent).save();
      } else if (this.createPdfString === true){
        console.log('%cCreate PDF in memory', 'color: green;');
        const pdf = await html2pdf().set(options).from(pdfContent).outputPdf();
        this.$emit('pdf-done', btoa(pdf));
      }
    },
  },
};
</script>
<style scoped>
.top-buttons{
  margin-bottom: 10px;
}
.pdf-container{
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  width: fit-content;
  margin: auto;
  margin-bottom: 50px;
}
.pdf-content{
  height: 1120px !important;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  height: 100%;
}

.top-graphix{
  transform: rotate(125deg);
  position: absolute;
  top: -230px;
}
.bottom-graphix{
  position: absolute;
  bottom: 10px;
  right: 10px;

  background-color: white;

  height: 140px;
}
.single-card{
  overflow: hidden;
  position: relative;
  
}
.content{
  position: absolute;
  top: 100px;
  left: 10px;
  height: 100px;
  line-height: 30px;
  font-size: 20px;

  display: flex;
  flex-direction: column;
  width: 92%;
}
.content-row{
  display: flex;
  flex-direction: row;
  margin: 5px 0 10px 0;
}
.content-row::before{
  content: 'a';
  opacity: 0;
}
.dashes{
  flex-grow: 1;
  border-bottom: 1px dashed black;
}
.single-card:nth-child(odd){
  border-right: 1px dashed lightgray;
}
.single-card:nth-child(1), .single-card:nth-child(2){
  border-bottom: 1px dashed lightgray;
}
</style>
