<template>
    <div>
        <!-- router absent du menu -->
        <h2 class="mb">Publiez une compétence !</h2>

        <div class="post">

            <h3>Publier un langage :</h3>
            <div>
                <form>
                    <input type="text" placeholder="ex:javascript" v-model="languageTitle">
                    <input type="text" placeholder="URL image" v-model="languageImage">
                    <input type="text" placeholder="Ajouter une description" v-model="languageDesc">
                </form>
                <div>
                    <button @click="postLanguage()">Envoyer</button>
                </div>
            </div>

            <h3>Publier une technologie :</h3>
            <div>
                <form>
                    <input type="text" placeholder="ex:sass" v-model="technologyTitle">
                    <input type="text" placeholder="URL image" v-model="technologyImage">
                    <input type="text" placeholder="Ajouter une description" v-model="technologyDesc">
                </form>
                <div>
                    <button @click="postTechnology()">Envoyer</button>
                </div>
            </div>

            <h3>Publier un concept :</h3>
            <div>
                <form>
                    <input type="text" placeholder="ex:seo" v-model="conceptTitle">
                    <input type="text" placeholder="URL image" v-model="conceptImage">
                    <input type="text" placeholder="Ajouter une description" v-model="conceptDesc">
                </form>
                <div>
                    <button @click="postConcept()">Envoyer</button>
                </div>
            </div>

            <h3>Publier un logiciel :</h3>
            <div>
                <form>
                    <input type="text" placeholder="ex:vscode" v-model="softwareTitle">
                    <input type="text" placeholder="URL image" v-model="softwareImage">
                    <input type="text" placeholder="Ajouter une description" v-model="softwareDesc">
                </form>
                <div class="mb">
                    <button @click="postSoftware()">Envoyer</button>
                </div>
            </div>
        </div>

        <div>
            <h4 class="second-title line-top">Modification/Suppression des publications :</h4>
            <h5>Langages :</h5>
            <div v-for="language in fetchLanguages" :key="language.id">
                <h6>{{language.title}}</h6>
                <img v-bind:src="language.img" alt="image language" class="img">
                <p>{{language.text}}</p>

                <button v-on:click="displayLanguages()">Afficher la modification</button>
                <div v-if="showLanguages">
                    <form>
                        <input type="text" placeholder="ex:html/css" v-model="languageTitle">
                        <input type="text" placeholder="URL image" v-model="languageImage">
                        <input type="text" placeholder="Ajouter une description" v-model="languageDesc">
                        <br>
                        <button @click="updateLanguages(language.id)">Modifier</button>
                    </form>
                </div>

                <button @click="deleteLanguages(language.id)">Supprimer</button>
            </div>

            <h5>Technologies :</h5>
            <div v-for="technology in fetchTechnologies" :key="technology.id">
                <h6>{{technology.title}}</h6>
                <img v-bind:src="technology.img" alt="image technology" class="img">
                <p>{{technology.text}}</p>

                <button v-on:click="displayTechnologies()">Afficher la modification</button>
                <div v-if="showTechnologies">
                    <form>
                        <input type="text" placeholder="ex:bootstrap" v-model="technologyTitle">
                        <input type="text" placeholder="URL image" v-model="technologyImage">
                        <input type="text" placeholder="Ajouter une description" v-model="technologyDesc">
                        <br>
                        <button @click="updateTechnologies(technology.id)">Modifier</button>
                    </form>
                </div>

                <button @click="deleteTechnologies(technology.id)">Supprimer</button>
            </div>

            <h5>Concepts :</h5>
            <div v-for="concept in fetchConcepts" :key="concept.id">
                <h6>{{concept.title}}</h6>
                <img v-bind:src="concept.img" alt="image concept notion" class="img">
                <p>{{concept.text}}</p>

                <button v-on:click="displayConcepts()">Afficher la modification</button>
                <div v-if="showConcepts">
                    <form>
                        <input type="text" placeholder="ex:w3c" v-model="conceptTitle">
                        <input type="text" placeholder="URL image" v-model="conceptImage">
                        <input type="text" placeholder="Ajouter une description" v-model="conceptDesc">
                        <br>
                        <button @click="updateConcepts(concept.id)">Modifier</button>
                    </form>
                </div>

                <button @click="deleteConcepts(concept.id)">Supprimer</button>
            </div>

            <h5>Logiciels :</h5>
            <div v-for="software in fetchSoftwares" :key="software.id">
                <h6>{{software.title}}</h6>
                <img v-bind:src="software.img" alt="image software" class="img">
                <p>{{software.text}}</p>

                <button v-on:click="displaySoftwares()">Afficher la modification</button>
                <div v-if="showSoftwares">
                    <form>
                        <input type="text" placeholder="ex:postman" v-model="softwareTitle">
                        <input type="text" placeholder="URL image" v-model="softwareImage">
                        <input type="text" placeholder="Ajouter une description" v-model="softwareDesc">
                        <br>
                        <button @click="updateSoftwares(software.id)">Modifier</button>
                    </form>

                </div>
                <button @click="deleteSoftwares(software.id)">Supprimer</button>
            </div>

            <div class="mb"></div>
        </div>
    </div>
</template>

<script>
    import axios from "axios"

    export default {
        name: "CRUD",
        data() {
            return {
                // Données à afficher
                languageTitle: "",
                languageImage: "",
                languageDesc: "",

                technologyTitle: "",
                technologyImage: "",
                technologyDesc: "",

                conceptTitle: "",
                conceptImage: "",
                conceptDesc: "",

                softwareTitle: "",
                softwareImage: "",
                softwareDesc: "",

                // Tableau vide pour stocker dans les requêtes
                fetchLanguages: [],
                fetchTechnologies: [],
                fetchConcepts: [],
                fetchSoftwares: [],

                // Afficher le bouton pour modifier
                showLanguages: false,
                showTechnologies: false,
                showConcepts: false,
                showSoftwares: false
            }
        },
        methods: {
            // Post
            postLanguage() {
                axios.post("http://localhost:3000/languages", {
                    title: this.languageTitle,
                    img: this.languageImage,
                    text: this.languageDesc
                }).then((res) => {
                    console.log(res);
                }).catch((err) => {
                    console.error(err);
                })
            },
            postTechnology() {
                axios.post("http://localhost:3000/technologies", {
                    title: this.technologyTitle,
                    img: this.technologyImage,
                    text: this.technologyDesc
                }).then((res) => {
                    console.log(res);
                }).catch((err) => {
                    console.error(err);
                })
            },
            postConcept() {
                axios.post("http://localhost:3000/concepts", {
                    title: this.conceptTitle,
                    img: this.conceptImage,
                    text: this.conceptDesc
                }).then((res) => {
                    console.log(res);
                }).catch((err) => {
                    console.error(err);
                })
            },
            postSoftware() {
                axios.post("http://localhost:3000/softwares", {
                    title: this.softwareTitle,
                    img: this.softwareImage,
                    text: this.softwareDesc
                }).then((res) => {
                    console.log(res);
                }).catch((err) => {
                    console.error(err);
                })
            },
            // Get
            getLanguages() {
                axios.get("http://localhost:3000/languages").then((res) => {
                    console.log(res.data)
                    this.fetchLanguages = res.data
                }).catch((err) => {
                    console.error(err)
                })
            },
            getTechnologies() {
                axios.get("http://localhost:3000/technologies").then((res) => {
                    console.log(res.data)
                    this.fetchTechnologies = res.data
                }).catch((err) => {
                    console.error(err)
                })
            },
            getConcepts() {
                axios.get("http://localhost:3000/concepts").then((res) => {
                    console.log(res.data)
                    this.fetchConcepts = res.data
                }).catch((err) => {
                    console.error(err)
                })
            },
            getSoftwares() {
                axios.get("http://localhost:3000/softwares").then((res) => {
                    console.log(res.data)
                    this.fetchSoftwares = res.data
                }).catch((err) => {
                    console.error(err)
                })
            },
            // Update
            updateLanguages(id) {
                axios.patch(`http://localhost:3000/languages/${id}`, {
                    title: this.languageTitle,
                    img: this.languageImage,
                    text: this.languageDesc
                }).then((res) => {
                    console.log(res.data)
                    this.getLanguages();
                }).catch((err) => {
                    console.error(err)
                })
            },
            updateTechnologies(id) {
                axios.patch(`http://localhost:3000/technologies/${id}`, {
                    title: this.technologyTitle,
                    img: this.technologyImage,
                    text: this.technologyDesc
                }).then((res) => {
                    console.log(res.data)
                    this.getTechnologies();
                }).catch((err) => {
                    console.error(err)
                })
            },
            updateConcepts(id) {
                axios.patch(`http://localhost:3000/concepts/${id}`, {
                    title: this.conceptTitle,
                    img: this.conceptImage,
                    text: this.conceptDesc
                }).then((res) => {
                    console.log(res.data)
                    this.getConcepts();
                }).catch((err) => {
                    console.error(err)
                })
            },
            updateSoftwares(id) {
                axios.patch(`http://localhost:3000/softwares/${id}`, {
                    title: this.softwareTitle,
                    img: this.softwareImage,
                    text: this.softwareDesc
                }).then((res) => {
                    console.log(res.data)
                    this.getSoftwares();
                }).catch((err) => {
                    console.error(err)
                })
            },
            // Delete
            deleteLanguages(id) {
                axios.delete(`http://localhost:3000/languages/${id}`).then((res) => {
                    console.log(res);
                    this.getLanguages() // Récupère l'id pour le supprimer
                }).catch((err) => {
                    console.error(err);
                })
            },
            deleteTechnologies(id) {
                axios.delete(`http://localhost:3000/technologies/${id}`).then((res) => {
                    console.log(res);
                    this.getTechnologies()
                }).catch((err) => {
                    console.error(err);
                })
            },
            deleteConcepts(id) {
                axios.delete(`http://localhost:3000/concepts/${id}`).then((res) => {
                    console.log(res);
                    this.getConcepts()
                }).catch((err) => {
                    console.error(err);
                })
            },
            deleteSoftwares(id) {
                axios.delete(`http://localhost:3000/softwares/${id}`).then((res) => {
                    console.log(res);
                    this.getSoftwares()
                }).catch((err) => {
                    console.error(err);
                })
            },
            // Display on click
            displayLanguages() {
                this.showLanguages = !this.showLanguages
            },
            displayTechnologies() {
                this.showTechnologies = !this.showTechnologies
            },
            displayConcepts() {
                this.showConcepts = !this.showConcepts
            },
            displaySoftwares() {
                this.showSoftwares = !this.showSoftwares
            }
        },
        mounted() {
            this.getLanguages()
            this.getTechnologies()
            this.getConcepts()
            this.getSoftwares()
        }
    }
</script>

<style scoped>
    /* Gestion formulaire */
    form {
        margin: 1rem 2.5rem 1rem 2.5rem;
        background-color: #FAFAFA;
        box-shadow: 1px 1px 1px 1px gray;
        border-radius: 2rem;
        padding: 1rem;
        opacity: 0.8;
    }

    input {
        border: 1px solid black;
        background: linear-gradient(#3CB371, white);
        margin: 0.6rem;
        padding: 0.4rem 0.8rem;
        border-radius: 1rem;
        font-size: 14px;
        font-family: 'Alegreya', serif;
    }

    button {
        margin: 1rem;
        padding: 0.4rem 1.4rem;
        border-radius: 2rem;
        color: white;
        font-size: 17px;
        font-family: 'Alegreya', serif;
        box-shadow: 1px 1px 1px 1px #3CB371;
        background: linear-gradient(#3CB371, black);
        opacity: 0.8;
    }

    button:hover {
        transform: scale(1.1);
        transition: 400ms linear;
    }

    button:active {
        transform: scale(1.2);
        transition: 300ms linear;
    }

    /* Gestion des titres et sous-titres */
    h2 {
        margin-top: 7rem;
        font-size: 2.5rem;
        font-family: 'Corinthia', cursive;
    }

    h3 {
        text-decoration: underline;
        font-size: 2rem;
        margin-top: 2.5rem;
        font-family: 'Alegreya', serif;
    }

    h5 {
        text-decoration: underline;
        font-size: 1.8rem;
        margin-top: 2.5rem;
        font-family: 'Alegreya', serif;
    }

    h6 {
        color: crimson;
        font-size: 1.5rem;
        margin-top: 2rem;
        font-family: 'Alegreya', serif;
    }

    .second-title {
        font-size: 2rem;
        padding-top: 3rem;
        color: black;
        font-family: 'Alegreya', serif;
        font-style: italic;
    }

    .post {
        border-width: 2px;
        border-style: dotted;
        border-color: black;
        margin: 0rem 1rem;
    }

    /* CSS partagé avec le composant Forum : */
    p {
        font-size: 1.3rem;
        font-style: italic;
        font-family: 'Alegreya', serif;
        margin-top: 1rem;
    }

    img {
        margin-top: 1rem;
        width: 80%;
        max-width: 200px;
        height: auto;
    }

    .line-top {
        width: 90%;
        margin-left: auto;
        margin-right: auto;
        border-top: 4px solid darkred;
        margin: 1rem 0rem;
    }

    .line-bottom {
        width: 75%;
        margin-left: auto;
        margin-right: auto;
        border-bottom: 2px solid gray;
    }

    .mb {
        margin-bottom: 3rem;
    }
</style>