<script lang="ts">
    import Registration from "../Components/Registration.svelte";
    import StudentList from "../Components/StudentList.svelte";
    import type { Student } from "../Models/Register";
	  // import { isEditing } from './../store/store.js';
    let Students:Student[] = [];
    let studentData:Student={
      id: Date.now(),
      name:"",
      gender:"",
      age:0,
      country: "",
      state: "",
      city: "",
    };
    let isEditing:boolean;
    let editStudentId:any;
    // console.log(editStudentId);
    // function to empty data from the input fields when user submitted the from//
  function empty(){
      studentData={
      id: Date.now(),
      name:"",
      gender:"",
      age:0,
      country: "",
      state: "",
      city: "",
    };
    }
    function HandleFromData(){
      let checkingId=studentData.id;
        console.log(checkingId);
        var index=Students.findIndex((student)=>student.id===checkingId)
        console.log(index);
     if (index !== -1) {
      // Update the student data in the list
      Students[index] = { ...studentData };
      // Reset form data after updating
      empty();
          isEditing=false;
          editStudentId=undefined;
          alert("student update successfully ")
    }
      else{
        console.log("New studentData",studentData);
        Students=[...Students,studentData];
        console.log("New Stdudent",Students);
        empty();
          alert("student register successfully ")
      }  
    }
    // display the information of student which is going to edit //
   function StudentInfoEdit(studentId:any){
    console.log(studentId.detail)
    const selectedStudent = Students.find(student => student.id === studentId.detail);
    console.log(selectedStudent)
    if (selectedStudent) {
      studentData = { ...selectedStudent };
    }
    isEditing=true;
    editStudentId=selectedStudent;
   }
   //delete button function //
   function StudentInfoDelete(id:any){
    console.log(id.detail);
    Students=Students.filter(item=>item.id!=id.detail)
   }
</script>
<div class="grid grid-cols-6 gap-4">
<div class="col-span-2">
    {#if editStudentId}
  <h1 class="text-xl mx-8 my-5">Update Student Details</h1>
  {:else}
  <h1 class="text-xl mx-8 my-5">Save Student Details</h1>
  {/if}
<Registration bind:studentData on:formData={HandleFromData} isEditingValue={isEditing}/>
</div>
<div class="col-span-3">
     <StudentList students={Students} on:edit={StudentInfoEdit} on:delete={StudentInfoDelete}/>
</div>
</div>
<style >
  :global(html) {
    background-color:grey;
  }
</style>