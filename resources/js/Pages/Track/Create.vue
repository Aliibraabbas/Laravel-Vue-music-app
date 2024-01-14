<template>
    <MusicLayout>
        <template #title>
            Créer un nouveau titre
        </template>
        <template #action>
            
        </template>
        <template #content>
            <form @submit.prevent="submit">
                <div class="mb-3">
                    <label class="block text-gray-700 text-sm font-bold mb-2" for="title">
                        Titre
                    </label>
                    <input
                        id="title"
                        v-model="form.title"
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline border-red-500"
                        :class="{ 'border-red-500': form.errors.title }"
                        type="text"
                        placeholder="Title"
                    >
                    <p class="text-red-500 text-xs italic">{{ form.errors.title }}</p>   
                </div>

                    <!-- Artist input -->
                <div class="mb-3">
                    <label class="block text-gray-700 text-sm font-bold mb-2" for="artist">
                        Artist
                    </label>
                    <input
                        id="artist"
                        v-model="form.artist"
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline border-red-500"
                        :class="{ 'border-red-500': form.errors.artist }"
                        type="text"
                        placeholder="Artist"
                    >
                    <p class="text-red-500 text-xs italic">{{ form.errors.artist }}</p>  
                </div>

                    <!-- Image input -->
                <div class="mb-3">
                    <label class="block text-gray-700 text-sm font-bold mb-2" for="image">
                        Miniature
                    </label>
                    <input
                        id="image"
                        @change="handleInputChange($event, 'image')"
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline border-red-500"
                        :class="{ 'border-red-500': form.errors.image }"
                        type="file"
                        accept="image/*"
                    >
                    <p class="text-red-500 text-xs italic">{{ form.errors.image }}</p>  
                </div>

                    <!-- Music input -->
                <div class="mb-3">
                    <label class="block text-gray-700 text-sm font-bold mb-2" for="music">
                        Music
                    </label>
                    <input
                        id="music"
                        @change="handleInputChange($event, 'music')"
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline border-red-500"
                        :class="{ 'border-red-500': form.errors.music }"
                        type="file"
                        accept="audio/*"
                    >
                        <p class="text-red-500 text-xs italic">{{ form.errors.music }}</p>
                </div>

                    <!-- Display input -->
                <div class="mb-3">
                    <label class="block text-gray-700 text-sm font-bold mb-2" for="display">
                        Display
                    </label>
                    <select
                        id="display"
                        v-model="form.display"
                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline border-red-500"
                        :class="{ 'border-red-500': form.errors.display }"
                    >
                        <option value="true">Yes</option>
                        <option value="false">No</option>
                    </select>
                    <p class="text-red-500 text-xs italic">{{ form.errors.display }}</p> 
                </div>

                <input type="submit" value="Submit" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded cursor-pointer">
            </form>
            
        </template>
    </MusicLayout>
</template>
   
<script>
   import MusicLayout from '@/Layouts/MusicLayout.vue'
   export default {
       components: { MusicLayout },
       data() {
           return {
               form: this.$inertia.form({
                  title: '',
                  artist: '',
                  image: null,
                  music: null,
                  display: true,
               })
           }
       },
       methods: {
           handleInputChange(event, fieldName) {
               this.form[fieldName] = event.target.files[0];
           },
           submit() {
                this.form.post(route('tracks.store'), {
                     onSuccess: () => this.$inertia.visit(route('track.index')),
                });
           }
       }
   }
</script>
   
