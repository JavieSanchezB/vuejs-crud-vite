<script setup>
import BreezeAuthenticatedLayout from '@/Layouts/Authenticated.vue';
import { Head, Link, useForm, lv, pv  } from '@inertiajs/inertia-vue3';


defineProps({
    posts: Array,
    laravelVersion: String,
    phpVersion: String
});
const form = useForm();
function destroy(id) {
    if (confirm("¿Estás seguro de que quieres eliminar?")) {
        form.delete(route('posts.destroy', id));
    }
}
</script>
<template>
    <Head title="Dashboard" />
    <BreezeAuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Laravel {{ laravelVersion }} PHP {{ phpVersion }}  VueJS CRUD App usando Vite 
            </h2>
        </template>
        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200">
                        <div className="flex items-center justify-between mb-6">
                            <Link
                                className="px-6 py-2 text-white bg-green-500 rounded-md focus:outline-none"
                                :href="route('posts.create')"
                            >
                               Crear Publicaciones 
                            </Link>
                        </div>
                        <table className="table-fixed w-full">
                            <thead>
                                <tr className="bg-gray-100">
                                    <th className="px-4 py-2 w-20">No.</th>
                                    <th className="px-4 py-2">Título</th>
                                    <th className="px-4 py-2">Publicación</th>
                                    <th className="px-4 py-2">Acción</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="post in posts">
                                    <td className="border px-4 py-2">{{ post.id }}</td>
                                    <td className="border px-4 py-2">{{ post.title }}</td>
                                    <td className="border px-4 py-2">{{ post.body }}</td>
                                    <td className="border px-4 py-2">
                                        <Link
                                            tabIndex="1"
                                            className="px-4 py-2 text-sm text-white bg-blue-500 rounded"
                                            :href="route('posts.edit', post.id)"
                                        >
                                            Editar
                                        </Link>
                                        <button
                                            @click="destroy(post.id)"
                                            tabIndex="-1"
                                            type="button"
                                            className="mx-1 px-4 py-2 text-sm text-white bg-red-500 rounded"
                                        >
                                            Borrar
                                        </button>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

      
    </BreezeAuthenticatedLayout>
</template>
