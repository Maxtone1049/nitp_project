<template>


    <!-- Contact Start -->
    <div class="container-xxl py-5">
        <div class="container">
            <div class="text-center wow fadeInUp" data-wow-delay="0.1s">
                <h6 class="section-title bg-white text-center text-primary px-3">Login</h6>
                </div>
            <div class="row g-4">
               
                <div class="col-lg-4 col-md-6 wow fadeInUp" data-wow-delay="0.3s">

                </div>
                <div class="col-lg-4 col-md-12 wow fadeInUp" data-wow-delay="0.5s">
                    <form id="loginForm" @submit.prevent="login">
                        <div class="row g-3">
                            <div class="col-12">
                                <div class="form-floating">
                                    <input type="email"  v-model="email" class="form-control" id="email" placeholder="Your Email" required>
                                    <label for="email">Email</label>
                                </div>
                            </div>
                            <div class="col-12">
                                <div class="form-floating">
                                    <input type="password" v-model="password" class="form-control" id="password" placeholder="Password" required>
                                    <label for="password">Password</label>
                                </div>
                            </div>
                            <div class="col-12">
                                <button class="btn btn-primary w-100 py-3 rounded-3" type="submit">Proceed</button>
                            </div>
                            <div class="col-12 text-center" id="loginMessage"></div>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
    <!-- Contact End -->



</template>


<script>


export default {
    name:'loginPage',

    

    data:() => {
        return {
            email:'',
            password:'',
            error:null
        };
    },


    methods: {
        login() {

            fetch("https://projectbackend-7waf.onrender.com/api/users/login", {

                method: "POST",
                headers: {
                "Accept":"application/json",
                "Content-Type": "application/json",
                },

                body:JSON.stringify({
                    email:this.email,
                    password:this.password
                })
            })
            .then(res => res.json())
            .then((res) => {

                if (!res.accessToken) {
                    this.error = res.message
                }else{
                    localStorage.setItem('authUser', res.accessToken);
                    
                    // console.log(localStorage);
                    this.$router.push({name:'heritagePage'})
                }

                

                
            })

        }
        
    },


    mounted() {
        let user = localStorage.getItem('user-info');
        // console.log(user);
        if (user) {
            this.$router.push({name:'homepage'})
        }
    },
}


</script>



<style scoped>


</style>