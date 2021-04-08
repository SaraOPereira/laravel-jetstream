<template>
    <app-layout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Cars
            </h2>
        </template>
        <div class="container">
            <div class="grid">
                <table class="table-auto">
                    <thead>
                        <tr>
                            <th v-for="column in columns" :key="column">{{ column }}</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>Intro to CSS</td>
                            <td>Adam</td>
                            <td>858</td>
                        </tr>
                        <tr class="bg-emerald-200">
                            <td>A Long and Winding Tour of the History of UI Frameworks and Tools and the Impact on Design</td>
                            <td>Adam</td>
                            <td>112</td>
                        </tr>
                        <tr>
                            <td>Intro to JavaScript</td>
                            <td>Chris</td>
                            <td>1,280</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </app-layout>
</template>

<script>
    import AppLayout from '@/Layouts/AppLayout'

    export default {
        props: ['sessions', 'columns'],
    
        components: {
            AppLayout
        }
    }
</script>