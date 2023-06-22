<template lang="">
    <div>
        <div class="container px-5 py-8 mx-auto flex flex-wrap">
            <div class="w-full h-full px-4 pt-4 pb-24">
                <div class=" bg-slate-100 px-8 py-8 relative border border-slate-200 roundedshadow shadow-slate-100 rounded">
                    
                    <form @submit.prevent="updateNote">
                    <div class="mb-6">
                        <h1 class="font-bold text-center text-2xl mb-4 pb-4 border-b border-slate-300">Edit Note</h1>
                        <label for="title" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">
                            Note Title
                        </label>
                        <input type="text" v-model="note.title" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-indigo-500 focus:border-indigo-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-indigo-500 dark:focus:border-indigo-500" placeholder="Your note title" required>
                    </div>
                    <div class="mb-6">                        
                        <label for="content" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">
                            Note Content
                        </label>
                        <textarea rows="6" v-model="note.content" class="block p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-indigo-500 focus:border-indigo-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-indigo-500 dark:focus:border-indigo-500" placeholder="Your note content..."></textarea>
                    </div>
                    <div v-if="isLoading" class="mb-4">
                        <Loading :title="isLoadingTitle"/>
                    </div>
                    <div v-else>
                    <button type="submit" class="text-white bg-indigo-700 hover:bg-indigo-800 focus:ring-4 focus:outline-none focus:ring-indigo-300 font-medium rounded-lg text-md w-full sm:w-auto mb-2 mr-2 px-5 py-2 text-center dark:bg-indigo-600 dark:hover:bg-indigo-700 dark:focus:ring-indigo-800">
                        Update Note
                    </button>
                    <Button to="/" type="button" class="text-white bg-red-700 hover:bg-red-800 focus:ring-4 focus:outline-none focus:ring-red-300 font-medium rounded-lg text-md w-full sm:w-auto px-5 py-2 text-center dark:bg-red-600 dark:hover:bg-red-700 dark:focus:ring-red-800">
                        <nuxt-link to="/">Cancel</nuxt-link>
                    </Button>
                    </div>
                    </form>

                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name:"noteEdit",
    data(){
        return {
            noteId: '',
            note: {},
            isLoading: false,
            isLoadingTitle: "Loading..."
        }
    },

    mounted(){
        this.noteId = this.$route.params.id;
        this.getNote(this.noteId);
    },

    methods:{
        getNote(noteId){
            this.isLoading = true;
            axios.get(`http://localhost:8000/api/notes/${noteId}/edit`).then(res => {
                console.log(res);
                this.isLoading = false;
                this.note = res.data.note;
            });
        },

        updateNote(){
            this.isLoading = true;
            this.isLoadingTitle = "Updating...";

            axios.put(`http://localhost:8000/api/notes/${this.noteId}/edit`, this.note).then(res => {
                console.log(res, 'res');
                alert(res.data.message);

                this.isLoading = false;
                this.isLoadingTitle = "Loading...";
                return navigateTo('/');
            });
        }
    },
}
</script>

<style lang="">
    
</style>