<template>
  <link
    href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css"
    rel="stylesheet"
    integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3"
    crossorigin="anonymous"
  />

  <div>
    
    <h1>Kayıt</h1>
    

    <form>
        <div class="form-group">
            <label>İsim</label>
            <input aria-label="İsim" placeholder="İsminizi giriniz" type="text" class="form-control" v-model="myname"/>

            <label>Mail</label>
            <input aria-label="mail" placeholder="rosa34@gmail.com" type="text" class="form-control" v-model="myemail"/>

            <label>Parola</label>
            <input  type="password" placeholder="Parolanızı giriniz" class="form-control" v-model="mypassword"/>
        
        
            
            <label>Parametreler</label>
            <input placeholder="host" type="list" class="form-control" v-model="myhost"/>
            <input placeholder="port" type="list" class="form-control" v-model="myport"/>
            <input placeholder="database adı" type="list" class="form-control" v-model="mydatabaseName"/>
            <input placeholder="ref" type="list" class="form-control" v-model="myref"/>
            <!-- <input placeholder="type" type="list" class="form-control" v-model="mytype"/> -->

            <label>Type</label>
            <div class="row">

              <form>
              
              <input type="radio" id="array" name="fav_language" value="array" v-model="mytype">
              <label for="array">array</label><br>
              
              <input type="radio" id="list" name="fav_language" value="list" v-model="mytype">
              <label for="list">list</label><br>
              

              <input type="radio" id="object" name="fav_language" value="object" v-model="mytype">
              <label for="object">object</label>
            </form>
            </div>
            
            
            
        </div>    
            <!--<input placeholder="selectedMemberships" type="list" class="form-control" v-model="myhost"/>-->
    </form>


            
        

       <div class="row">
            <!-- panel-footer -->
            <div class="col-6 text-left">
                <div class="previous">
                    <button @click="add"  type="submit" class="btn btn-primary pull-left">Kaydet<span class=""></span></button>
                    
                </div>
            </div>
            <div class="col-6 text-right">
                <div class="next">
                    <button @click="cancellation"  type="submit" class="btn btn-primary pull-right">İptal<span class=""></span></button>

                </div>
            </div>
        </div>

      <div>
        <u1>
            <li v-for="user of users" :key="user.id">
                
                {{ user.userName +" --> Host: "+user.parameters.host+ " Port: "+user.parameters.port + " -->Type:"+ user.parameters.selectedMemberships.type}}                
                
            </li>
        </u1>
        
      </div> 
    


    
    
  </div>
</template>

<script>
import axios from "axios";
const baseURL = "http://localhost:3001/users";


export default {
  name: "Users",
  data() {
    return {
      users: [],
      myname:"",
      myemail:"",
      mypassword:"",
      myhost:"",
      myport:"",
      mydatabaseName:"",
      mytype:"",
      myref:"",
      save: true,
    };
  },

  async created() {
    try {
      const res = await axios.get(baseURL);
      this.users = res.data;
    } catch (e) {
      console.error(e);
    }
  },
  methods: {
      async add(){
          
        try{
        const res= await axios.post(baseURL, {userName: this.myname ,email: this.myemail, password:this.mypassword, parameters:{host: this.myhost, port: this.myport,databaseName:this.mydatabaseName ,selectedMemberships:{type:this.mytype,ref:this.myref}}});
          this.users=[...this.users,res.data];

          this.myname="";
          this.myemail="";
          this.mypassword="";
          this.myhost="";
          this.myport="";
          this.mydatabaseName="";
          this.mytype="";
          this.myref="";


          }catch (e) {
              console.error(e);
          }
          
          
      },
      async cancellation(){
          this.myname="";
          this.myemail="";
          this.mypassword="";
          this.myhost="";
          this.myport="";
          this.mydatabaseName="";
          this.mytype="";
          this.myref="";

      }

  }

};
</script>

<style scoped>
h1 {
  text-decoration: underline;
}

li {
  color: white;
}




.btn-text-left{
	text-align: left;	
}
.btn-text-right{
	text-align: right;
}
 
 
.btn-text-center{
	text-align: center;	
}

</style>
