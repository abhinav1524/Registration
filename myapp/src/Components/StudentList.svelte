<script lang="ts">
	import type { Student } from './../Models/Register.ts';
    import { createEventDispatcher } from 'svelte';
    export let students:Student[] = [];
    const dispatch = createEventDispatcher();
   function handleEdit(studentId:any) {
    dispatch('edit', studentId);
  }
  function handleDelete(studentId:any){
    dispatch("delete",studentId);
  }
</script>
  <div class="overflow-x-auto">
        <table class="table-auto w-full border-collapse border border-gray-300">
            <thead>
                <tr class="bg-gray-200">
                    <th class="px-4 py-2">Name</th>
                    <th class="px-4 py-2">Gender</th>
                    <th class="px-4 py-2">Age</th>
                    <th class="px-4 py-2">Country</th>
                    <th class="px-4 py-2">State</th>
                    <th class="px-4 py-2">City</th>
                    <th class="px-4 py-2">Edit</th>
                    <th class="px-4 py-2">Delete</th>
                </tr>
            </thead>
           <tbody>
    {#each students as student}
        <tr class="bg-white border border-gray-300">
            <td class="px-4 py-2">{student.name}</td>
            <td class="px-4 py-2">{student.gender}</td>
            <td class="px-4 py-2">{student.age}</td>
            <td class="px-4 py-2">{student.country}</td>
            <td class="px-4 py-2">{student.state}</td>
            <td class="px-4 py-2">{student.city}</td>
            <td class="px-4 py-2"><button class="border-solid border-2 border-sky-500 px-5 py-2 bg-green-700 rounded-md text-white " on:click={()=>handleEdit(student.id)}>Edit</button></td>
            <td class="px-4 py-2"><button class="border-solid border-2 border-sky-500 px-5 py-2 bg-red-500 rounded-md text-white " on:click={()=>handleDelete(student.id)}>Delete</button></td>
        </tr>
    {/each}
</tbody>

        </table>
    </div>
<style>
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
</style>