<template>
  <div class="main-section">
    <section class="main-content">
      <h1>My settings</h1>
        <h2>Personal Data</h2>
        <div class="main-data-holder">
          <app-data-field
            v-for="(data, dataKey) in fullName"
            v-bind:dataKey="dataKey"
            v-bind:key="dataKey"
            v-bind:inputData="data"
            v-on:dataChanged="changeName">
          </app-data-field>
          <app-date-field
            v-on:dataChanged="changeName"
            v-bind:placeholder="dateOfBirth.placeholder"
            v-bind:inputData="dateOfBirth.value">
          </app-date-field>
        </div>
        <h2>Contact Data</h2>
        <div class="main-data-holder">
          <app-tel-field
            v-on:dataChanged="changeName"
            v-bind:inputData="tel">
          </app-tel-field>
          <app-email-field
            v-on:dataChanged="changeName"
            v-bind:inputData="email">
          </app-email-field>
          <app-psw-field
            v-on:dataChanged="changeName"
            v-bind:inputData="password">
          </app-psw-field>
        </div>
        <h2>Address</h2> 
        <app-address-book></app-address-book>
        
        <div class="notification-block">
          <h2>Notifications</h2>
          <label class="notification-block__label">
            <input class="notification-block__checkbox" type="checkbox" name="mail" checked>
              Notify current promotions by mail
          </label>
          <label class="notification-block__label">
            <input class="notification-block__checkbox" type="checkbox" name="sms" checked>
              Notify current promotions by Sms          
          </label>
        </div>        
    </section>
    <aside class="main-sidebar">
      <div class="social-block">
        <h3 class="social-block__heading">Socials</h3>
        <small class="social-block__sub-heading">Link your social network account to use as login</small>
        <a href="#facebook" class="social-block__item social-block__item_fb">
          <span class="social-block__icon social-block__icon_fb"></span>Facebook
        </a>
        <a href="#vkontakte" class="social-block__item social-block__item_vk">
          <span class="social-block__icon social-block__icon_vk"></span>Вконтакте
        </a>
        <a href="#twitter" class="social-block__item social-block__item_tw">
          <span class="social-block__icon social-block__icon_tw"></span>Twitter
        </a>
        <a href="#ok" class="social-block__item social-block__item_ok">
          <span class="social-block__icon social-block__icon_ok"></span>Одноклассники
        </a>
      </div>
    </aside>
  </div>
</template>

<script>
  import IMask from 'imask';

  import DataField from './components/dataField.vue';
  import DateField from './components/dateField.vue';
  import TelField from './components/telField.vue';
  import EmailField from './components/emailField.vue';
  import PasswordField from './components/pswField.vue';
  import AddressBook from './components/addressBook.vue';

  export default {
    data () {
      return {
        appName: 'RunWay Test Task',
        fullName: {
          Name: 'Dmitry',
          Surname: '',
          Patronymic : '',
        },
        // 2018-07-22
        dateOfBirth: {
          value : '',
          placeholder: 'Date of Birth'
        },
        tel: '',
        email: 'dmitriy_loginov@gmail.com',
        password: ''
      }
    },
    methods: {
      changeName(input){
        this.testvalue = input;
      }
    },
    components: {
      AppDataField: DataField,
      AppDateField: DateField,
      AppTelField: TelField,
      AppEmailField: EmailField,
      AppPswField: PasswordField,
      AppAddressBook: AddressBook
    }
  }
</script>

<style lang="scss">
  html, body{
    font-family: Verdana;
    background-color: #f4f4f4;
    color: #333333;
  }

  h1{
    font-size: 22px;
    text-transform: uppercase;
    margin-bottom: 30px;
  }

  h2{
    font-size: 18px;
    margin-bottom: 18px;
  }

  h3{
    margin: 0;
    font-size: 14px;
  }

  input, button{
    outline-color: #e5e5e5;
  }

  small {
    font-size: 12px;
  }

  .btn-holder{
    display: flex;
    
    &_flex-end{
      justify-content: flex-end;
    }
  }

  .main-section{
    display: flex;
    justify-content: space-between;
    max-width: 920px;
    margin: 0 auto;
  }
  .main-content{
    width: 600px;
  }
  .main-sidebar{
    width: 290px;
  }
  .main-data-holder{
    border: solid 1px #d5d5d5;
    background-color: #fff;
    margin-bottom: 50px; 
  }

  .data-field{
    display: flex;
    align-items: center;
    justify-content: space-between;

    transition: background 300ms ease-in;

    font-size: 12px;
    padding: 14px 20px;

    &_active{
      padding: 10px 20px 10px 14px;
      background-color: #f1f1f1;
    }

    &:not(:last-child){
      border-bottom: solid 1px #d5d5d5;
    }

    &:hover{
      background-color: #f1f1f1;
    }

    &__value{
      
      &_type{
        
        &_empty{
          color: #aaaaaa;
        }
      }
    }

    &__input{
      padding: 4px 6px;
      width: 45%;
      border: solid 1px #d5d5d5;
    }
    &__btn{
      transition: all 300ms ease-in;

      cursor: pointer;
      // outline: 1px solid #666;
      
      border: none;
      background: none;

      font-size: 12px;
      color: #aaaaaa;
      text-decoration: underline;

      &:hover, &_active{
        color: #e85a22;
      }
    }
  }

  .notification-block{
    display: flex;
    flex-direction: column;

    font-size: 14px;

    &__label{
      display: flex;
      align-items: center;

      cursor: pointer;

      margin-bottom: 8px;
    } 

    &__checkbox{
      margin-right: 10px;
    }
  }

  .social-block{
    margin-top: 50px;
    padding: 20px;
    background-color: #fff6e0;

    &__heading{
      margin-bottom: 16px;
    }

    &__sub-heading {
      display: inline-block;
      margin-bottom: 16px;
    }

    &__item{
      display: flex;
      align-items: center;
      width: 100%;
      height: 40px;
      margin-bottom: 10px;
      
      font-size: 12px;
      text-decoration: none;
      color: #fff;
      background-color: #e5e5e5;

      &_fb{
        background-color: #1d59a3;
      }
      &_vk{
        background-color: #1c608d;
      }
      &_tw{
        background-color: #00b2e6;
      }
      &_ok{
        background-color: #ef7800;
      }
    }
    &__icon{
      width: 24px;
      height: 20px;
      margin: 0 10px;

      background-position: center;
      background-repeat: no-repeat;

      &_fb{
        background-image: url(./assets/img/fb.png);
      }
      &_vk{
        background-image: url(./assets/img/vk.png);
      }
      &_tw{
        background-image: url(./assets/img/tw.png);
      }
      &_ok{
        background-image: url(./assets/img/ok.png);
      }
    }    
  }

  @media screen and (max-width: 900px){
    .main-section{
      max-width: 900px;
      padding: 0px 10px;
    }

    .main-content{
      width: 60%;
    }  
    .main-sidebar{
      width: 35%;
    }

    .data-field__input {
      width: 65%;
    }
  }

  @media screen and (max-width: 560px){
    .main-section{
      flex-direction: column;
      max-width: 460px;
      padding: 0px 10px;
    }

    .main-content{
      margin-bottom: 20px;
    }
    .main-content,
    .main-sidebar{
      width: 100%;
    }

    .social-block{
      margin: 0 auto;
      max-width: 360px;
    }

    
  }
  @media screen and (max-width: 360px){
    h1,h2,h3{
      text-align: center;
    }

    .notification-block__label{
      justify-content: center;
    }  
  }
</style>
