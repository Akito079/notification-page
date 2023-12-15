<template>
   <!-- main content wrapper -->
   <section class="max-w-[1024px] mx-auto bg-white rounded-lg shadow-lg p-8">
    <!-- noti header -->
    <div class="flex items-center justify-between">
      <div class="flex items-center">
        <span class="text-2xl font-bold">Notification</span>
        <span class="inline-block bg-blue-500 text-white font-medium rounded-full px-2 mx-2 ">{{ notiCount }}</span>
      </div>
      <button  class="font-medium text-gray-500" @click="readAllMessage()">Mark all as read</button>
    </div>
    <!-- noti body -->
    <div class="flex flex-col">
      <div class="">
        <div
          v-for="(noti,index) in notifications"
          :key="noti.id"
          class="flex  justify-between my-3 gap-2 rounded-xl p-5 shadow-md cursor-pointer"
          :class="{'bg-gray-100': noti.readStatus }"
          @click="readNoti(index)"
        >
          <div class="flex gap-2">
            <img :src="'../../images/'+noti.image" class="w-10 h-10 shadow-sm" alt="" />
            <div class="flex flex-col">
              <div class="flex items-center w-full">
                <p :class="{'dot-red' : noti.readStatus }">
                  <span class="font-bold">{{ noti.name }}</span> {{ noti.action }}
                  <span class="font-bold">{{ noti.target }}</span>
                </p>
              </div>
              <div class="">
                <small class="text-gray-400 font-semibold">{{ noti.time }}</small>
              </div>
              <div v-if="noti.message"
                class="my-5 border p-3 border-gray-400 rounded-md text-gray-500 font-semibold hover:bg-gray-100  cursor-pointer "
              >
                {{ noti.message }}
              </div>
            </div>
          </div>
          <div class="" v-if="noti.postImage" >
            <img :src="'../../images/'+noti.postImage" class="w-12 h-12" alt="" />
          </div>
        </div>

      </div>
    </div>
  </section>
</template>
<script setup>
import notification from "@/scripts/notification";
import { ref,computed }from "vue";
const notifications = ref(notification);
function readNoti(i){
  notifications.value[i].readStatus = false;
}
const notiCount = computed(()=>{
  const readMessageCount =  notifications.value.filter((item)=>
      item.readStatus === true
  )
  return readMessageCount.length
});

function readAllMessage(){
 notifications.value.forEach(item => {
  item.readStatus = false ;
 });
}
</script> 
