<template>
  <div class="data-field"
        v-bind:class="{'data-field_active' : !showData}">
    <span class="data-field__value"
          v-show="showData"
          v-bind:class="{'data-field__value_type_empty' : this.maskValue === this.placeholder}">
      {{ maskValue }}
    </span>
    <input type="date" class="data-field__input"
            v-show="!showData"
            v-bind:class="{'data-field__input_disabled' : showData}"
            v-bind:value="outputData"
            v-on:input="inputValue"
            v-bind:disabled="showData" /> 
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
    placeholder: String,
    inputData: String
  },
  data(){
    return {
      outputData: this.inputData,
      maskValue: '',
      showData: true,
      state: 'edit'
    }
  },
  // # переосмыслить
  created: function(){
    if(this.outputData){
      let dateStr = this.inputData;
      let date = dateStr.split('-');
      this.maskValue = date[2] + '.' + date[1] + '.' + date[0];
    } else if(this.placeholder){
      this.maskValue = this.placeholder;
    }
  },
  methods:{
    inputValue($event){
       let dateStr = $event.target.value;
       if(dateStr){
         let date = dateStr.split('-');

         this.maskValue = date[2] + '.' + date[1] + '.' + date[0];
         this.outputData = dateStr;
       } else {
         this.maskValue = this.placeholder;
         this.outputData = '';
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
  },
}

</script>

<style lang="scss" scoped>
  .data-field{

    &__input{
      color: #bdbdbd;
    }
  }
</style>