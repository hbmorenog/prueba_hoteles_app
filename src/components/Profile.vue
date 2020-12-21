<template>
        <div id="Profile">
        <h2 class="mb-3">Hi  <span> {{name}} </span>,  Welcome!</h2>
        <ul>
            <li>Ubication: {{ubication}}</li>
            <li>Email: {{email}}</li>
            <li>Price: {{price}}</li>
        </ul>
    <b-row>
        <b-col class="md-6">
            <p class="pr-5 pl-5">{{description}}</p>
        </b-col>
    </b-row>
    </div>

</template>



<script>
    import axios from 'axios';
    export default {
        name: 'Profile',
        data: function (){
            return {
                email: "",
                ubication: "",
                name: "",
                price: 0,
                description: ""
            }
        },

        created: function(){
            this.email = this.$route.params.email

            let self = this
            axios.get("https://g3m3-e9-hoteles-api.herokuapp.com/hotel/profile/" + this.email)
                .then((result) => {
                    self.ubication = result.data.ubication;
                    self.name = result.data.name;
                    self.price = result.data.price;
                    self.description = result.data.description;
                })
                .catch((error) => {
                    alert("ERROR Servidor");
                });
        }
    }
</script>

<style>
    #Profile{
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    #Profile h2{
        font-size: 50px;
        color: #283747;
    }

    #Profile span{
        color: crimson;
        font-weight: bold;
    }
</style>