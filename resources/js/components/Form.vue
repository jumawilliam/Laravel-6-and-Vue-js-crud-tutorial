<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">New company</div>
                    
                    <div class="card-body">
                    	<div v-for="s in success" class="alert alert-success">
                    		<strong>{{s}}</strong>
                    	</div>
                    	<div v-for="e in errors" class="alert alert-danger">
                    		<strong>{{e}}</strong>
                    	</div>
                       <form>
                       	Name:<input type="text" v-model="name" class="form-control">
                       	Phone:<input type="text" v-model="phone" class="form-control">
                       	Email: <input type="email" v-model="email" class="form-control">
                       	<input type="submit" @click.prevent="createcompany">
                       </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
    	data(){
    		return{
    		  success:null,
    		  errors:null,
              name:'',
              phone:'',
              email:''
    		}
    	},
    	methods:{
    		createcompany(){
    			if(!this.name){
    				this.errors=['Name Cannot be empty']
    				return false;
    			}
    			if(!this.phone){
    				this.errors=['Phone cannot be empty']
    				return false;
    			}
    			if(!this.email){
    				this.errors=['Email cannot be empty']
    				return false;
    			}else if(!this.validEmail(this.email)){
    				this.errors=['Please enter a valid email']
    				return false;
    			}
    			axios.post('/company',{name:this.name,email:this.email,phone:this.phone}).then(response=>{
    				
    				this.success=response.data;
    				
    			}).catch(errors=>{
    				this.errors=errors.data;
    			});
    			    this.name='';
    				this.email='';
    				this.phone='';
    			    


    		},
			    		validEmail: function (email) {
			    var re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
			    return re.test(email);
			}
    	},
    	
        mounted() {
            alert('Welcome')
        }
    }
</script>
