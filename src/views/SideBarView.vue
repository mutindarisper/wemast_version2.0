<template>
    <div id="sidebar" class="leaflet-sidebar collapsed">
    <!-- Nav tabs -->
    <div class="leaflet-sidebar-tabs">
        <ul role="tablist" class="no_display"> <!-- top aligned tabs -->
            <li><a href="#home1" role="tab"><i class="fa fa-bars"></i></a></li>
            <li class="disabled"><a href="#messages" role="tab"><i class="fa fa-envelope"></i></a></li>
            <li><a href="#profile" role="tab"><i class="fa fa-user"></i></a></li>
        </ul>
 
        <ul role="tablist" class="no_display"> <!-- bottom aligned tabs -->
            <li><a href="#settings" role="tab"><i class="fa fa-gear"></i></a></li>
        </ul>
    </div>
 
    <!-- Tab panes -->
    <div class="leaflet-sidebar-content">
        <div class="leaflet-sidebar-pane" id="home1">
            <!-- <h1 class="leaflet-sidebar-header">
                sidebar-v2
                <div class="leaflet-sidebar-close"><i class="fa fa-caret-left"></i></div>
            </h1>
            <p>A responsive sidebar for mapping libraries</p> -->
        </div>
 
        <div class="leaflet-sidebar-pane" id="messages">
            <!-- <h1 class="leaflet-sidebar-header">Messages<div class="leaflet-sidebar-close"><i class="fa fa-caret-left"></i></div></h1> -->
        </div>
 
        <div class="leaflet-sidebar-pane" id="profile">
            <!-- <h1 class="leaflet-sidebar-header">Profile<div class="leaflet-sidebar-close"><i class="fa fa-caret-left"></i></div></h1> -->
        </div>
    </div>
</div>
  
</template>

<script setup>

</script>

<style scoped>
.no_display{
    display: none;
}
</style>