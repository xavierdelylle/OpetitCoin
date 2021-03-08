<template>
  <div>
    <main class="Main-article">       
      <h2>Créer un article</h2>   
      <form @submit.prevent="addToilette">
        <fieldset>
          <div class="articleAdd">
            <div class="field">
              <label class="field__label">titre</label>
              <input class="field__input" type="text" placeholder="toilette deluxe" v-model="toilette.title" />
            </div> 
            <div class="field field__file">
              <label>File
                <input type="file" class="inputfile" name="featured"  accept="image/*" @change="handleFileChange($event)">
              </label>                
            </div>                                                      
            <div class="field">
              <label class="field__label">description</label>
                <textarea
                  placeholder="RTFM" v-model="toilette.content"
                  class="field__input"
                  style="height: 10em;">
                </textarea>
            </div>  
            <div class="formRadio">
              <div class="field">
                <label class="field__label">Lieux</label>
                <div>
                  <input type="radio" id="13" v-bind:value="13" v-model="toilette.place">
                  <label for="chez bidule">chez bidule</label>

                  <input type="radio" id="5" v-bind:value="5" v-model="toilette.place">
                  <label for="privée">privée</label>

                  <input type="radio" id="6" v-bind:value="6" v-model="toilette.place">
                  <label for="public">public</label>
                </div>
              </div>
              <div class="field">
                <label class="field__label">Type d'utilisateurs</label>
                <div>
                  <input type="radio" name="action1" id="7" v-bind:value="7" v-model="toilette.toilette_utilisateurs">
                  <label for="femme">femme</label>
                        
                  <input type="radio" name="action2" id="4" v-bind:value="4" v-model="toilette.toilette_utilisateurs">
                  <label for="mixte">mixte</label>

                  <input type="radio" name="action3" id="2" v-bind:value="2" v-model="toilette.toilette_utilisateurs">
                  <label for="homme">homme</label>

                  <input type="radio" name="action4" id="9" v-bind:value="9" v-model="toilette.toilette_utilisateurs">
                  <label for="PMR">PMR</label>

                  <input type="radio" name="action5" id="8" v-bind:value="8" v-model="toilette.toilette_utilisateurs">
                  <label for="espace bébé">espace bébé</label>
                </div>
              </div>
            </div>
          </div>
        </fieldset>       
        <button class="button">Envoyer la demande d'ajout</button>
      </form> 
    </main>
  </div>
</template>

<script>
import ToiletteService from '../services/ToiletteService'

export default {
    name: 'ArticleCreate',
       data(){
        return {
            toilette:{},
            }
    },
    methods: {
      handleFileChange($event){
        console.log("test",$event)
        this.toilette.featured = $event.target.files[0];
      },  
      addToilette() {        
          console.log("here 2", this.toilette)

          ToiletteService.uploadPicture(this.toilette)
          .then((res) => {
            let mediaId = res.data.id;
            this.toilette.featured_media = mediaId;
            ToiletteService.createToilette(this.toilette)
          }  )
          .catch(err => console.log(err))
      }    
  },
}


</script>

<style scoped lang="scss">

@import "../assets/scss/variables";
@import "../assets/scss/mixins";
@import "../assets/scss/forms";



.field__file {

    input[type=file] :focus + label{
      background-color: $ButtonLogin;
      color: $TextConnect;
    }
}
</style>