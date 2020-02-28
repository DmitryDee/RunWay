<template>
  <div class="address-book"
        v-bind:class="{ 'address-book_active' : showEditAddress }">
    <div class="address-book__header">
      <h3>Current delivery address</h3>
      <button class="data-field__btn"
              v-bind:class="{'data-field__btn_active' : showEditAddress}"
              v-on:click="showEditBlock"> 
      {{ state }}
      </button>
    </div>
    <div class="address-book__address-holder">
      <div class="address-book__data-group"
            v-for="address in addressData">
        <label class="address-book__data">
        <input class="address-book__radio"
                type="radio" 
                name="address"
                v-bind:id="address.id" >
        	{{ address.index + ' ' + address.country + ', ' + address.city + ', ' + address.data }}
        </label>
        <button class="data-field__btn"
            v-show="showEditAddress"
            v-on:click="deleteAddress(address.id)"> 
          delete
        </button>
      </div>
    </div>
    <div class="address-book__edit-block"
          v-show="showEditAddress">
      <h3 class="address-book__edit-header">Add new address</h3>
      <div class="address-book__input-holder">
        <input type="text"
                maxlength="7"
                class="address-book__input"
                v-bind:value="inputIndex"
                v-on:input="saveIndex">  
        <select class="address-book__input"
                name="country"
                v-model="selectedCountry">
          <option value="" disabled selected>Country</option>
          <option value="Russia">Russia</option>  
        </select>
        <select class="address-book__input"
                name="city"
                v-model="selectedCity">
          <option value="" disabled selected>City</option>
          <option value="Moskow">Moskow</option>
          <option value="Saint-Petersburg">Saint-Petersburg</option>
        </select>  
      </div>
      <input type="text"
              class="address-book__input address-book__input_type_address"
              v-model="inputAddress">    
    </div>
    <div class="btn-holder"
          v-bind:class="{ 'btn-holder_flex-end' : showEditAddress}">
      <button
        class="address-book__btn"
        v-on:click="pushAddress"
        v-bind:disabled="!showEditAddress">
        {{ !showEditAddress ? 'Add another address' : 'Add address' }}
      </button>
    </div>
  </div>
</template>

<script>
let masked = IMask.createMask({
  mask: '000 000',
});

export default{
  props: {

  },
  data(){
    return {
      state: 'edit',
      showEditAddress: false,
      inputIndex: '',
      inputAddress: '',
      selectedCountry: '',
      selectedCity: '',
      addressData: [
        {
          id: 0,
          index: '432 071',
          country: 'Россия',
          city: 'г. Троицк',
          data : 'ул. Ленина д.34. кв.54',
        },
        {
          id: 1,
          index: '445 086',
          country: 'Россия',
          city: 'г. Керчь',
          data: 'ул. Первого Интернационала д.14. кв.6',
        }
      ]
    }
  },
  created(){

  },
  methods:{
    pushAddress(){
      if(this.inputIndex && this.selectedCountry && this.selectedCity && this.inputAddress){
        this.addressData.push({
          id: (this.addressData.length + 1),
          index: this.inputIndex,
          country:  this.selectedCountry,
          city: this.selectedCity,
          data: this.inputAddress,
        });
      }
    },
    deleteAddress(id){
      let items = this.addressData;
      for(let i = 0; i < items.length; i++){
        if(i == id){
          items.splice(i, 1);
        }
      }
      for(let i= 0; i < items.length; i++){
        items[i].id = i;
      }
    },
    showEditBlock(){
      this.state = (this.state == 'edit') ? 'save' : 'edit';
      this.showEditAddress = !this.showEditAddress;
    },
    saveIndex($event){
      this.inputIndex = masked.resolve($event.target.value);
    }
  },
  computed: {
  },
}

</script>

<style lang="scss">
  .address-book{
    transition: all 300ms ease-in;

    background-color: #fff;
    border: solid 1px #d5d5d5;
    padding: 14px;

    &_active{
      background-color: #f1f1f1;
    }
    
    &__header{
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px;  
    }

    &__edit-block{
      padding-top: 10px; 
      border-top: solid 1px #d5d5d5;
    }

    &__edit-header{
      margin-bottom: 20px;
      text-transform: uppercase;
    }
    
    &__data-group{
      display: flex;
      flex-wrap: nowrap;
      justify-content: space-between;
      align-items: center;

      margin-bottom: 10px;
    }

    &__data{
      cursor: pointer;
      display: flex;
      align-items: center;
      font-size: 12px;
    }

    &__address-holder{
      margin-bottom: 18px;
    }

    &__input-holder{
      display: flex;
      justify-content: space-between;

      margin-bottom: 12px;
    }

    &__input{
      width: 28%;
      border: solid 1px #d5d5d5;
      
      font-size: 12px;
      padding: 4px 6px;
      
      &_type_address{
        width: 100%;
        box-sizing: border-box;

        margin-bottom: 20px;
      }
    }
    

    &__radio{
      cursor: pointer;
      margin-right: 10px;
    }


    &__btn{
      cursor: pointer;
      transition: all 300ms ease-in;

      padding: 10px 8px;
      background-color: #e85a22;
      border: 1px solid #bbbbbb;
      color: #fff;
      font-size: 12px;

      &:disabled{
        background-color: #cdc9c7;
      }
    }
  }
</style>