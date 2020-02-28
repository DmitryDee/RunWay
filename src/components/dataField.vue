<template>
  <div class="data-field"
        v-bind:class="{'data-field_active' : !showData}">
    <span class="data-field__value"
          v-show="showData"
          v-bind:class="{'data-field__value_type_empty' : outputData === dataKey}">
      {{ outputData }}
    </span>
    <input type="text" class="data-field__input"
            v-show="!showData"
            v-bind:value="checkOutput" 
            v-on:input="inputValue"/> 
    <button class="data-field__btn"
            v-bind:class="{'data-field__btn_active' : !showData}"
            v-on:click="changeState"> 
      {{ state }}
    </button>
  </div>
</template>

<script>

export default{
  props: {
    dataKey: String,
    inputData: String,
    inputType: String
  },
  data(){
    return {
      outputData: (this.inputData) ? this.inputData : this.dataKey,
      showData: true,
      state: 'edit'
    }
  },
  created(){

  },
  methods:{
    inputValue($event){
      let value = $event.target.value;
      if(value){
        this.outputData = $event.target.value;
      } else {
        this.outputData = this.dataKey;
      }
    },
    changeState(){
      this.state = (this.state == 'edit') ? 'save' : 'edit';
      this.showData = !this.showData;
      if(this.outputData !== this.inputData){
        this.$emit('dataChanged', this.outputData);
      }
    }
  },
  computed: {
    checkOutput(){
      return (this.outputData == this.dataKey) ? '' : this.outputData;
    }
  },
}

</script>

<style lang="scss" scoped>
  
</style>