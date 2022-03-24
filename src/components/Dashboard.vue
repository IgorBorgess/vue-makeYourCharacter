<template>
    <div id="sheet-table">
        <Message v-bind:msg="msg" v-show="msg" />
        <div>
            <div id="sheet-table-heading">
                <div class="order-id">#:</div>
                <div>Name:</div>
                <div>Race:</div>
                <div>Class:</div>
                <div>Proficiencies:</div>
                <div>Actions:</div>
            </div>
        </div>
        <div id="sheet-table-rows">
            <div class="sheet-table-row" v-for="approvedsheet in approvedsheets" v-bind:key="approvedsheet.id">
                <div class="order-number">{{approvedsheet.id}}</div>
                <div>{{approvedsheet.name}}</div>
                <div>{{approvedsheet.race}}</div>
                <div>{{approvedsheet.classification}}</div>
                <div>
                    <ul>
                        <li v-for="(proficiency, index) in approvedsheet.proficiencies" v-bind:key="index">{{proficiency}}</li>
                    </ul>
                </div>
                <div>
                    <select name="status" class="status" @change="updateSheets($event, approvedsheet.id)">
                        <option value="">Status</option>
                        <option v-for="s in status" v-bind:key="s.id" v-bind:value="s.tipo"
                        v-bind:selected="approvedsheet.status === s.tipo">{{s.tipo}}</option>
                    </select>
                    <button class="delete-btn" @click="deleteSheet(approvedsheet.id)">Delete</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Message from "./Message.vue"
export default {
    name: "Dashboard",
    components: {
        Message
    },
    data() {
        return {
        approvedsheets: null,
        approvedsheets_id: null,
        status: [],
        msg: null
        }
    },
    methods: {
        async getSheets() {
            const req = await fetch("http://localhost:3000/approvedsheets")
            const data = await req.json()

            this.approvedsheets = data
            console.log(this.approvedsheets)

            // resgatar os status
            this.getStatus()
        },
        async getStatus() {
            const req = await fetch("http://localhost:3000/status")
            const data = await req.json()

            this.status = data
        },
        async deleteSheet(id) {
            // Msg de sistema
            this.msg = `The sheet of ID ${id} was repproved and therefore deleted.`
            //Limpar msg
            setTimeout(() => this.msg = "", 3000);

            const req = await fetch(`http://localhost:3000/approvedsheets/${id}`, {
            method: "DELETE"})
            const res = await req.json()

            this.getSheets()
        },
        async updateSheets(event, id) {
            const option = event.target.value

            const dataJson = JSON.stringify({ status: option })
            const req = await fetch(`http://localhost:3000/approvedsheets/${id}`, {
                method: "PATCH",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            })
            const res = await req.json()

            // Msg de sistema
            this.msg = `The sheet of ID ${res.id} was updated to ${res.status}!`
            //Limpar msg
            setTimeout(() => this.msg = "", 3000);
        }
    },
    mounted() {
        this.getSheets()
    }
}
</script>

<style scoped>

    #sheet-table {
    max-width: 1200px;
    margin: 0 auto;
    font-size: 28px;
    }
    #sheet-table-heading,
    #sheet-table-rows,
    .sheet-table-row {
        display: flex;
        flex-wrap: wrap;
    }
    #sheet-table-heading {
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid #333;
    }
    .sheet-table-row {
        width: 100%;
        padding: 12px;
        border-bottom: 1px solid #CCC;
    }
    #sheet-table-heading div,
    .sheet-table-row div {
        width: 19%;
    }
    #sheet-table-heading .order-id,
    .sheet-table-row .order-number {
        width: 5%;
    }
    select {
        padding: 12px 6px;
        margin-right: 12px;
        border-style: solid;
    }
    .delete-btn {
        background-color: #222;
        color:red;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }
    .delete-btn:hover {
        background-color: transparent;
        color: #222;
    }
    @font-face {
    font-family: "DND-Text";
    src: url("../../public/fonts/Draconis.ttf") format("truetype");
    }

</style>