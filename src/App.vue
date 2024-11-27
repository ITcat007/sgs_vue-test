<template>
  <div class="container">
    <div class="selects">
      <form action="#" @submit.prevent="saveData">
        <app-select 
          :options="citiesData" 
          name="city" 
          defaultOptionText="Город"
          v-model="selectedCity"
          @update:modelValue="onCityChange"
        />
        
        <app-select
          :options="filteredDepartments"
          name="department" 
          defaultOptionText="Цех"
          v-model="selectedDepartment"
          @update:modelValue="onDepartmentChange"
         />
        
        <app-select 
          :options="filteredEmployees" 
          name="employee" 
          defaultOptionText="Сотрудник"
          v-model="selectedEmployee"
        />
                
        <app-select 
          :options="factoryTeamData" 
          name="team" 
          defaultOptionText="Бригада"
          v-model="selectedTeam"        
        />

        <app-select 
          :options="workShiftData" 
          name="shift" 
          defaultOptionText="Смена"
          v-model="selectedShift"  
        />

        <button class="btn-save">Отправить</button>
      </form>
    </div>
  </div>
</template>

<script>
  import AppSelect from './components/AppSelect.vue'

  export default{
    components: {
      AppSelect
    },
    data(){
      return {
        citiesData: [
          {id: "mos77", name: "Москва"},
          {id: "spb78", name: "Санкт-Петербург"},
          {id: "eka66", name: "Екатеринбург"}
        ],
        departmentsData: [
          { city_id: "mos77", id:"ABC123", name: "ABC123" },
          { city_id: "mos77", id:"DEF456", name: "DEF456" },
          { city_id: "mos77", id:"GHI789", name: "GHI789" },
          { city_id: "spb78", id:"JKL101", name: "JKL101" },
          { city_id: "spb78", id:"MNO202", name: "MNO202" },
          { city_id: "spb78", id:"PQR303", name: "PQR303" },
          { city_id: "eka66", id:"STU404", name: "STU404" },
          { city_id: "eka66", id:"VWX505", name: "VWX505" },
          { city_id: "eka66", id:"YZA606", name: "YZA606" }
        ],
        employeesData: [
          { dep_id: "ABC123", id: "SMI123", name: "Смирнов А.В." },
          { dep_id: "ABC123", id: "PET456", name: "Петров И.И." },
          { dep_id: "ABC123", id: "IVA789", name: "Иванов С.С." },
          
          { dep_id: "DEF456", id: "KUZ101", name: "Кузнецов А.П." },
          { dep_id: "DEF456", id: "SAV202", name: "Савельев Д.А." },
          { dep_id: "DEF456", id: "KRY303", name: "Крылов О.Н." },
          
          { dep_id: "GHI789", id: "LIT404", name: "Литвинов Р.М." },
          { dep_id: "GHI789", id: "ZAY505", name: "Зайцев И.В." },
          { dep_id: "GHI789", id: "NOV606", name: "Новиков К.О." },
          
          { dep_id: "JKL101", id: "TRO707", name: "Трофимов Н.Г." },
          { dep_id: "JKL101", id: "VAS808", name: "Васильев А.С." },
          { dep_id: "JKL101", id: "GOR909", name: "Гордеев И.П." },
          
          { dep_id: "MNO202", id: "PEL010", name: "Пелевин С.К." },
          { dep_id: "MNO202", id: "SER111", name: "Сергеев В.И." },
          { dep_id: "MNO202", id: "ESH222", name: "Ешев А.Н." },
          
          { dep_id: "PQR303", id: "TUL333", name: "Тулупов Ф.Р." },
          { dep_id: "PQR303", id: "CLI444", name: "Клименко Е.Н." },
          { dep_id: "PQR303", id: "RAL555", name: "Ралдугин В.И." },
          
          { dep_id: "STU404", id: "MAS666", name: "Масленников А.Д." },
          { dep_id: "STU404", id: "KHA777", name: "Харитонов Г.С." },
          { dep_id: "STU404", id: "FOM888", name: "Фомин Р.М." },
          
          { dep_id: "VWX505", id: "ZEF999", name: "Зефиров К.И." },
          { dep_id: "VWX505", id: "NEG000", name: "Негин В.П." },
          { dep_id: "VWX505", id: "BUL111", name: "Булатов Г.В." },
          
          { dep_id: "YZA606", id: "KIM222", name: "Кимов Р.С." },
          { dep_id: "YZA606", id: "CHE333", name: "Чернов И.Н." },
          { dep_id: "YZA606", id: "BLO444", name: "Блохин А.Е." }
        ],
        factoryTeamData: [
          {id: "ft01", name: "Специализированная"},
          {id: "ft02", name: "Комплексная"}
        ],
        workShiftData: [
          {id: "wsh01", name: "Дневная"},
          {id: "wsh02", name: "Ночная"}
        ],
        selectedCity: null,
        selectedDepartment: null,
        selectedEmployee: null,

        selectedTeam: null,
        selectedShift: null   
      }
    },

    methods: {  
      onCityChange(newCity){
        this.selectedCity = newCity;
        this.selectedDepartment = null;
        this.selectedEmployee = null;
      },

      onDepartmentChange(newDepartment){
        this.selectedDepartment = newDepartment;
        this.selectedEmployee = null;
      },

      saveData(){
        const outputObj = {
          city: this.selectedCity,
          department: this.selectedDepartment,
          employee: this.selectedEmployee,
          factoryTeam: this.selectedTeam,
          workShift: this.selectedShift
        };
        this.saveCookies('select_values', outputObj);
      },

      saveCookies(name, value){
        this.$cookies.set(name, value);
      }
    },
    computed: {
      filteredDepartments(){
        if(this.selectedCity !== null){
          return this.departmentsData.filter(department => department.city_id === this.selectedCity);
        }        
      },

      filteredEmployees() {
        if(this.selectedDepartment !== null){
          return this.employeesData.filter(employee => employee.dep_id === this.selectedDepartment);
        }
      }
    }
  }
</script>

<style>
  .container{
    max-width: 1140px;
    margin: 0 auto;
    text-align: center;
  }

  .selects{
    padding-top: 50px;
  }

  .btn-save{
    cursor: pointer;
    margin-top: 30px;
    padding: 10px 15px;
  }
</style>