<script>
export default {
  name: 'Flashcard',
    data() {
        return {
            newName: "",
            newNote: "",
            lists: [],
            add: false,
            item: null,
        }
    },
    methods: {
        card(toggler) {
           toggler.flash =  !toggler.flash
        },
        news() {
            this.add = true
        },
        done() {
            if(this.newName === "") {
                alert("Title Required")
                return;
            }
            this.lists.push(
                {
                    id: this.lists.length + 1,
                    name: this.newName,
                    note: this.newNote,
                    flash: true
                }
            );
            this.add = false
            this.newName = ""
            this.newNote = ""
             localStorage.setItem("lists", JSON.stringify(this.lists))
        },
        newInput(e) {
            this.newName = e.target.value
        },
        newNoteInput(e) {
            this.newNote = e.target.value;
        },
    },
    mounted() {
        this.item = JSON.parse(localStorage.getItem("lists"))
        if (this.item) {
            this.lists = this.item
        }
    },
}
</script>

<template>
    <div class="header">
        <h1>Vue Flashcards</h1>
        <h3>The Vue student preparatory</h3>
        <div class="line">
            <hr />
            <div class="button" @click="news"> &plus; </div>
            <hr />
        </div>
        <small>Click to toggle Show and Hide</small>
    </div>
    <div class="grid">
        <div v-for="list in lists" class="cards-card" @click="card(list)">
            <h1 v-if="list.flash"> {{ list.name }} </h1>
            <div v-else>
                <p>{{ list.note }}</p>
            </div>
            <!-- <div class="button2" @click="func">&minus;</div> -->
        </div>
    </div>
    <div v-show="add" class="add-card">
        <div class="wrapper">
            <h1>Add FlashCard</h1>
            <input type="text" placeholder="Title" @input="newInput">
            <textarea name="desc" id="1" cols="30" rows="10" placeholder="Notes" @input="newNoteInput"></textarea>
            <button @click="done">Submit</button>
        </div>
    </div>

</template>
<style scoped>
.header{
    text-align: center;
}
.add-card {
    position: fixed;
    top: 0;
    left: 0;
    background-color: #00000088;
    display: flex;
    height: 100vh;
    width: 100vw;
    z-index: 99;
    align-items: center;
    justify-content: center;
    backdrop-filter: blur(10px);
}
.wrapper{
    background-color: white;
    padding: 20px;
    display: flex;
    flex-direction: column;
    border-radius: 10px;
    width: 350px;
}
.wrapper input{
    padding: 10px;
    margin-block: 10px;
}
.wrapper textarea{
    padding: 10px;
}
.wrapper button{
    padding: 10px;
    margin-block: 10px;
    background-color: #7e87d6;
    border: 1px solid #7e87d655;
    border-radius: 2px;
}

.grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 20px;
    padding: 20px;
}
@media only screen and (min-width: 600px) {
    .grid {
        grid-template-columns: 1fr 1fr;
    }
}
@media only screen and (min-width: 800px) {
    .grid{
        grid-template-columns: 1fr 1fr 1fr;
    }
}

.line {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
}

.line hr {
    width: 40%;
    height: 0px;
    border: 4px solid #7e87d6;
    border-radius: 3px;
}

.button {
    font-size: 30px;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 70px;
    height: 60px;
    margin-inline: 10px;
    border: 1px solid transparent;
    border-radius: 50%;
    cursor: pointer;
    background-color: #7e87d6;
    color: white;
}


.cards-card {
    background-color: white;
    box-shadow: 0px 10px 20px #7e87d655;
    width: 250px;
    display: flex;
    flex-direction: column;
    height: 25vh;
    align-items: center;
    justify-content: center;
    padding: 20px;
}
</style>