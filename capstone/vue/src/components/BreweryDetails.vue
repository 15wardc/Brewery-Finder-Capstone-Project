<template>
      
   
    <div id="details">
<div class="heading">
      <h1 class="brewery-name">{{brewery.name}}</h1> 

    <h1 class="brewery-name">{{brewery.name}}</h1> 

<div class="address">
    <h2><span v-if="brewery.street" >{{brewery.street}}, </span>{{brewery.city}}</h2>
</div>

<div class="website">
    <a v-bind:href="brewery.websiteUrl" target="_blank"><h3> {{brewery.websiteUrl}}</h3></a>
</div>

<div class="description">
<h2>{{brewery.hoursOfOperation}}</h2>
</div>
</div>
<div class="buttons">
<button id="updatebrewery" @click="pushToUpdateBrewery" v-if="$store.state.user.role == 'ROLE_BREWER'">Update Brewery</button>
              <button id="deletebutton" v-if="$store.state.user.role == 'ROLE_BREWER'" v-on:click="deleteBrewery(brewery.id)">Delete Brewery</button>
<button id="addbeer" @click="pushToAddBeer" v-if="$store.state.user.role == 'ROLE_BREWER'">Add Beer</button>
</div>
<div class="subheading">
    <h3>Beers from {{brewery.name}}</h3>
</div>

</div>

</template>


<script>


import applicationService from "../services/ApplicationService";
export default {
   
    name: "brewery-details",
    
    data() {
        return {
           brewery: {
  id: "",
  brewerId: this.$store.state.user.id,
        name: "",
        street: "",
        city: "",
        state: "",
        phone: "",
        websiteUrl: "",
        hoursOfOperation: "",
},
            showForm: false,

        }

    },

    methods: {

        pushToAddBeer(){
            this.$router.push({name: 'beerform' });
        },

        pushToUpdateBrewery(){
            this.$router.push({name: 'updatebrewery' });
        },

deleteBrewery() {
      applicationService;
      if (
        confirm(
          "Are you sure you want to delete this brewery and all associated information? This action cannot be undone."
        )
      ) {
        applicationService
          .deleteBrewery(this.brewery.id)
          .then((response) => {
            if (response.status === 200) {
              alert("Brewery successfully deleted");

              this.$store.commit("DELETE_BREWERY", this.brewery.id);

              this.$router.push({ name: "home" });
            }
          })

          .catch((error) => {
            if (error.response) {
              this.errorMsg =
                "Error deleting brewery. Response received was '" +
                error.response.statusText +
                "'.";
            } else if (error.request) {
              this.errorMsg =
                "Error deleting brewery. Server could not be reached.";
            } else {
              this.errorMsg =
                "Error deleting brewery. Request could not be created.";
            }
          });
      }
    },
    },
   
    created() {
        this.brewery = this.$store.state.activeBrewery;
    }
}

</script>

<style scoped>

*{
    margin-left: 40px;
}


#addbeer{
    font-size: 5vh;
    display: flex;
    color: white;
}

#details {
  padding: 0;
  margin-bottom: -10vh;
  box-sizing: border-box;
  
}
.heading {
    display: grid;
    /* text-align: cente; */
    grid-template-columns: auto auto;
    margin-top: 100px;
    grid-column-gap: 1vw;
    background-color: #C0C0C0;
    margin: 15vh 20vw 0 20vw;
    border-radius: 15px;
    box-shadow: inset 0px 0px 10px #000;
}
.submitBtn {
    text-align: center;
    margin: 15px;
}
.subheading {
    color: 	#404040;
    font-size: 1.8rem;
    text-align: center;
    background-color: whitesmoke;
    background-position: center;
    margin: 8% 28% 5% 28%;
    border-radius: 15px;
    box-shadow: inset 0px 0px 10px #000;
}
@keyframes logo{
   0%{opacity: 0%; width: 0%;}
   20%{opacity: 20%; width: 20%;}
   40%{opacity: 40%; width: 40%;}
   60%{opacity: 60%; width: 60%;}
   80%{opacity: 80%; width: 80%;}
   100%{opacity: 100%; width: 100;}
}
#deletebutton{
  border: 7px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0px 0px 20px rgba(8, 7, 16, 0.6);
  color: darkgoldenrod;
  font-size: 110%;
  background-color: black;
  cursor: pointer;
  margin-top: 0.5vh;

}


.address{
    grid-column: 2/2;
    grid-row: 3/2;
    font-size: 12px;
    color: black;
    margin-top: -5vh;
    /* text-align: center; */
        transform: translate(-4vw, 1vh); 
}


.brewery-name {
    grid-column: 2/2;
    font-size: 3rem;
    grid-row: 1/1;
    text-align: center;
    margin-right: 50px;
    transform: translate(-3vw, 2vh);
}
.website {
    grid-column: 2/2;
    grid-row: 2/2;
    /* margin-top: 10vh; */
    text-align: center;
    transform: translate(-5.2vw, 5vh);
}
#updatebrewery{
   border: 7px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0px 0px 20px rgba(8, 7, 16, 0.6);
  color: darkgoldenrod;
  font-size: 110%;
  background-color: black;
  cursor: pointer;
  margin-left: 725px;
}
/* .address {
    grid-column: 2/2;
    grid-row: 2/2;
    font-size: 12px;
    color: black;
    margin-top: 2vh;
} */

a:link {
    text-decoration: none;
    color: black;
    font-size: 12px;
}
button{
    color: black;
}
a:hover {
    color: 	#696969;
}
.description {
    grid-column: 1/3;
    grid-row: 3/3;
    /* text-align: center; */
    margin: 2vh 2vw 0 2vw;
    transform: translate(-2vw, 2vh);

}

/* #beer-list {
    padding-top: 15px;
    text-align: center;
} */
/* .card-space {
    border-radius: 15px;
    margin-bottom: 10vh;
    box-shadow: inset 0px 0px 10px #000;
}
.card-space:nth-child(odd) {
    background-color: 	#C0C0C0;
}
.card-space:nth-child(even) {
    background-color: 	#F5F5F5;
} */
/* .card-space:hover {
    background-color: rgb(139, 139, 139);

} */

#addbeer{
    border: 7px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0px 0px 20px rgba(8, 7, 16, 0.6);
  color: darkgoldenrod;
  font-size: 110%;
  background-color: black;
  cursor: pointer;
  margin-left: 840px;
  margin-top: 2.5px;
 
}


</style>