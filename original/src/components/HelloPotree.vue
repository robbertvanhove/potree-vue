<template>
  <div class="potree_container" style="position: absolute; width: 100%; height: 100%; left: 0px; top: 0px; ">
    <div id="potree_render_area"></div>
    <div id="potree_sidebar_container"> </div>
    </div>
</template>

<script>
export default {
  name: 'HelloPotree',
  data () {
    return {
      msg: 'Welcome to Potree Vue.js App'
    }
  },
  mounted(){
    window.viewer = new Potree.Viewer(document.getElementById("potree_render_area"));
		
		viewer.setEDLEnabled(true);
		viewer.setFOV(60);
		viewer.setPointBudget(1*1000*1000);
		viewer.loadSettingsFromURL();
		
		viewer.setDescription("Loading Octree of LAS files");
		
		viewer.loadGUI(() => {
			viewer.setLanguage('en');
			$("#menu_appearance").next().show();
			//viewer.toggleSidebar();
		});
		
		// Sigeom
		Potree.loadPointCloud("static/pointclouds/lion_takanawa_las/cloud.js", "lion", function(e){
			viewer.scene.addPointCloud(e.pointcloud);
			
			let material = e.pointcloud.material;
			material.size = 1;
			material.pointSizeType = Potree.PointSizeType.ADAPTIVE;
			
			e.pointcloud.position.x += 3;
			e.pointcloud.position.y -= 3;
			e.pointcloud.position.z += 4;
			
			viewer.fitToScreen();
		});
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
