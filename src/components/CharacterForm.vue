<template>  
    <div>
        <Message v-bind:msg="msg" v-show="msg" />
        <div>
            <form id="character-form" @submit="createSheet">
                <div class="input-container">
                    <label for="name">Character's name:</label>
                    <input type="text" id="name" name="name" v-model="name" placeholder="Your Character's Name">
                </div>
                    <div class="input-container">
                    <label for="race">Choose the character's race:</label>
                    <select name="race" id="race" v-model="race">
                        <option value="">Select the race</option>
                        <option v-for="race in races" v-bind:key="race.id" v-bind:value="race.tipo">{{ race.tipo }}</option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="class">Choose the character's class:</label>
                    <select name="class" id="class" v-model="classification">
                        <option value="">Select the class</option>
                        <option v-for="classe in classifications" v-bind:key="classe.id" v-bind:value="classe.tipo">{{ classe.tipo }}</option>
                    </select>
                </div>
                <div class="input-container" id="proficiency-container">
                    <label id="proficiency-title" for="proficiency">Choose the character's proficiency:</label>
                    <div class="checkbox-container" v-for="proficiency in proficienciesdata" v-bind:key="proficiency.id">
                        <input type="checkbox" name="proficiency" v-model="proficiencies" v-bind:value="proficiency.tipo">
                        <span>{{proficiency.tipo}}</span>
                    </div>
                </div>
                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Create the character!">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import Message from "./Message.vue"

export default {
    name: "CharacterForm",
    components: {
        Message
    },

    data() {
        return {
            races: null,
            classifications: null,
            proficienciesdata: null,
            name: null,
            race: null,
            classification: null,
            proficiencies: [],
            msg: null
        }
    },
    methods: {
        async getSheets() {
            const req = await fetch("http://localhost:3000/sheets")
            const data = await req.json()

            this.races = data.races
            this.classifications = data.classifications
            this.proficienciesdata = data.proficiencies
        },
        async createSheet(event) {
            event.preventDefault()
            const data = {
                name: this.name,
                race: this.race,
                classification: this.classification,
                proficiencies: Array.from(this.proficiencies),
                status: "Requested"
            }
            const dataJson = JSON.stringify(data)

            const req = await fetch("http://localhost:3000/approvedsheets", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            })
            const res = await req.json()
            
            // Msg de sistema
            this.msg = `Character created! Please be patient while we'll see if ${res.name} is approved!`
            
            //Limpar msg
            setTimeout(() => this.msg = "", 3000);

            //Limpar campos
            this.name = ""
            this.race = ""
            this.classification = ""
            this.proficiencies = ""
        }
    },
    mounted() {
        this.getSheets()
    }
}
</script>

<style scoped>
    #character-form {
        max-width: 400px;
        margin: 0 auto;
    }

    .input-container {
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label {
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid red;
    }

    input, select {
        padding: 5px 10px;
        width: 300px;
    }

    #proficiency-container {
        flex-direction: row;
        flex-wrap: wrap;
    }

    #proficiency-title {
        width: 100%;
    }

    .checkbox-container {
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px;
    }

    .checkbox-container span,
    .checkbox-container input {
        width: auto;
    }

    .checkbox-container span {
        margin-left: 6px;
        font-weight: bold;
    }

    .submit-btn {
        background-color: #222;
        color: red;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }

    .submit-btn:hover {
        background-color: transparent;
        color: #222;
    }
</style>