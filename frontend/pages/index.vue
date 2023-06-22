<template lang="">
    <div>
        <!-- <h1>My Index page</h1> -->
        <div class="container px-5 py-8 mx-auto flex flex-wrap">
            <div v-if="isLoading" class="mb-4">
                <Loading title="Loading..."/>
            </div>
            <!-- <div > -->
                <div v-else v-for="(note, index) in notes" :key="index" class="h-full p-4 md:w-2/3 lg:w-1/3">
                    <div class=" bg-slate-100 px-8 py-8 relative border border-indigo-100 roundedshadow shadow-indigo-100 hover:shadow-lg hover:shadow-indigo-200">
                        <div>
                            <p class="hidden">{{ note.id }}</p>
                            <h1 class="title-font sm:text-2xl text-xl  mb-3 font-bold">{{ note.title }}</h1>
                            <p class="mb-3">
                                {{ note.content }}
                            </p>
                        </div>
                        <div class="flex justify-between mt-4">
                            <button type="button" @click="deleteNotes($event, note.id)" class="bg-red-700 text-slate-100 hover:text-slate-200 hover:bg-red-600 hover:shadow-md hover:shadow-red-700 px-4 py-1 rounded">Delete</button>
                            <NuxtLink :to="`/notes/${note.id}`"  class="bg-green-700 text-slate-100 hover:text-slate-200 hover:bg-green-600 hover:shadow-md hover:shadow-green-700 px-4 py-1 rounded">Edit</NuxtLink>
                        </div>
                    </div>
                </div>
            <!-- </div> -->
        </div>
    </div>
</template>
<script>
import axios from 'axios';

export default {
    name : "note",
    data() {
        return {
            notes:{},
            isLoading: true,
        }
    },
    mounted() {
        this.getNotes();
    },

    methods: {
        getNotes(){
            this.isLoading = true;
            axios.get(`http://localhost:8000/api/notes`).then(res => {
                // console.log(res.data.notes);
                this.isLoading = false;
                this.notes = res.data.notes;
            });
        },

        deleteNotes(event, noteId){
            if(confirm('Are you sure to delete this note?')){
                event.target.innerText = 'Deleting...';
                axios.delete(`http://localhost:8000/api/notes/${noteId}/delete`).then(res => {
                    event.target.innerText = 'Deleting...';
                    this.getNotes();
                    alert(res.data.message);
                })
            }
        }
    }
}
</script>
<style lang="">
    
</style>
