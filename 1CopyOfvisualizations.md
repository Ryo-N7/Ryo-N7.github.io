---
layout: gallery
title: Visualizations Gallery
css: "/css/materialize.css"
---

### WORK IN PROGRESS 
### COME BACK SOON


<div class="container center filter">
<div class="row">
  <form class="col s12">
	<div class="row">
	  
	  <div class="input-field col s2">
		<!-- <i class="material-icons prefix">sort_by_alpha</i> -->
		<select id="gridsort">
		  <option value="name">Name</option>
		  <option value="release">Release Date</option>
		  <option value="type">Type</option>
		  <!-- <option value="author">Author</option> -->
		  <!-- <option value="stars" selected>Github stars</option> -->
		  <!-- <option value="stars">Github stars</option> -->
		</select>
		<label>Sort</label>
	  </div>
	  
	  <div class="input-field col s4">
		<!-- <i class="material-icons prefix">search</i> -->
		<input type="text" id="textfilter" class="validate" placeholder="name, tag, description">
		<label>Text Filter</label>
	  </div>
	  
	  <div class="input-field col s3">
		<!-- <i class="material-icons prefix">sort_by_alpha</i> -->
		<select id="authorfilter">
		  <option value="" selected>&nbsp;</option>
		  <!-- <option value="author">Author</option> -->
		</select>
		<label>Type Filter</label>
	  </div>
	  
	  <div class="input-field col s3">
		<!-- <i class="material-icons prefix">sort_by_alpha</i> -->
		<select id="tagfilter">
		  <option value="" selected>&nbsp;</option>
		  <!-- <option value="author">Author</option> -->
		</select>
		<label>Tag Filter</label>
	  </div>
	  
	</div>
  </form>
</div>
</div>

<div class="main-container">
	<div class="row" id="grid">

		<!-- card: test -->
	
		<div class="card grid-item" data-author="ryo-nakagawara">
		  <div class="card-image waves-effect waves-block waves-light">
			<div style="width:350px; height:300px; padding:3px;" class="valign-wrapper">
			<a href="https://github.com/Ryo-N7/tidy_tuesday#april-3">
			<img class="valign" src="
			
			  /img/college_tuition_bumpchart.png
			
			"></a>
			</div>
		  </div>
		  <div class="card-content widget-content">
			<a href="https://github.com/Ryo-N7/tidy_tuesday#april-3"><span class="card-title grey-text text-darken-4">Average College Tuition in the USA (by state)</span></a>
			<p class="widget-shortdesc">Visualised by a bump chart showing top 10 states.
		</p>
			<p class="widget-list-item"><i class="material-icons meta-bullet red-text"></i><span class="red-text">type:</span> <span class="widget-author widget-meta">Visualization</span></p>
			<p class="widget-list-item"><i class="material-icons meta-bullet green-text"></i><span class="green-text">tags:</span> <span class="widget-tags widget-meta">bump-chart</span></p>
			<p class="widget-list-item"><i class="material-icons meta-bullet blue-text"></i><span class="blue-text">libraries:</span> <span class="widget-jslibs widget-meta">ggplot2</span>
			<span class="widget-release-nr">?</span>
		</p>
			<!-- <div class="more-icon activator"><i class="material-icons right">more_vert</i></div> -->
			<div class="hidden widget-cran">true</div>
		  </div>
		  <div class="card-reveal" style="display: none; -webkit-transform: translateY(0px);">
			<span class="card-title grey-text text-darken-4">phylocanvas<i class="material-icons right">close</i></span>
			<p>(full meta data to go here)</p>
			</div>
		</div>
		
		<!-- card: Calendar Heatmap -->
		
		<div class="card grid-item" data-author="ryo-nakagawara">
		  <div class="card-image waves-effect waves-block waves-light">
			<div style="width:350px; height:300px; padding:3px;" class="valign-wrapper">
			<a href="https://github.com/Ryo-N7/tidy_tuesday#april-16">
			<img class="valign" src="
			
			  /img/cause_of_death_east_africa.m4p
			
			"></a>
			</div>
		  </div>
		  <div class="card-content widget-content">
			<a href="https://github.com/Ryo-N7/tidy_tuesday#april-16"><span class="card-title grey-text text-darken-4">East Africa Deaths Boxplot</span></a>
			<p class="widget-shortdesc">Visualizing the median proportion of deaths in East Africa.
		</p>
			<p class="widget-list-item"><i class="material-icons meta-bullet red-text"></i><span class="red-text">type:</span> <span class="widget-author widget-meta">Visualisation</span></p>
			<p class="widget-list-item"><i class="material-icons meta-bullet green-text"></i><span class="green-text">tags:</span> <span class="widget-tags widget-meta">time-series</span></p>
			<p class="widget-list-item"><i class="material-icons meta-bullet blue-text"></i><span class="blue-text">libraries:</span> <span class="widget-jslibs widget-meta">ggplot2</span>
			<span class="widget-release-nr">1</span>
		</p>
			<!-- <div class="more-icon activator"><i class="material-icons right">more_vert</i></div> -->
			<div class="hidden widget-cran">true</div>
		  </div>
		  <div class="card-reveal" style="display: none; -webkit-transform: translateY(0px);">
			<span class="card-title grey-text text-darken-4">East Africa Deaths Boxplot<i class="material-icons right">close</i></span>
			<p>(full meta data to go here)</p>
			</div>
		</div>
		
		<!-- card: Global Terrorism -->
		
		<div class="card grid-item" data-author="dominik-koch">
		  <div class="card-image waves-effect waves-block waves-light">
			<div style="width:350px; height:300px; padding:3px;" class="valign-wrapper">
			<a href="https://datascience42.shinyapps.io/terrorism/">
			<img class="valign" src="
			
			  /img/Global-Terrorism.png
			
			"></a>
			</div>
		  </div>
		  <div class="card-content widget-content">
			<a href="https://datascience42.shinyapps.io/terrorism/"><span class="card-title grey-text text-darken-4">Global Terrorism App</span></a>
			<p class="widget-shortdesc"> Highlight global terrorism on an interactive map.
		</p>
			<p class="widget-list-item"><i class="material-icons meta-bullet red-text">stop</i><span class="red-text">type:</span> <span class="widget-author widget-meta">Dashboard</span></p>
			<p class="widget-list-item"><i class="material-icons meta-bullet green-text">stop</i><span class="green-text">tags:</span> <span class="widget-tags widget-meta">interactive-maps,time-series</span></p>
			<p class="widget-list-item"><i class="material-icons meta-bullet blue-text">stop</i><span class="blue-text">libraries:</span> <span class="widget-jslibs widget-meta">shiny,leaflet,timevis</span>
			<span class="widget-release-nr">2</span>
		</p>
			<!-- <div class="more-icon activator"><i class="material-icons right">more_vert</i></div> -->
			<div class="hidden widget-cran">true</div>
		  </div>
		  <div class="card-reveal" style="display: none; -webkit-transform: translateY(0px);">
			<span class="card-title grey-text text-darken-4">Global Terrorism App<i class="material-icons right">close</i></span>
			<p>(full meta data to go here)</p>
			</div>
		</div>
		
		<!-- card: Bump Chart -->
		
		<div class="card grid-item" data-author="dominik-koch">
		  <div class="card-image waves-effect waves-block waves-light">
			<div style="width:350px; height:300px; padding:3px;" class="valign-wrapper">
			<a href="https://dominikkoch.github.io/Bump-Chart/">
			<img class="valign" src="
			
			  /img/bumpChart_clean.png
			
			"></a>
			</div>
		  </div>
		  <div class="card-content widget-content">
			<a href="https://dominikkoch.github.io/Bump-Chart/"><span class="card-title grey-text text-darken-4">Bump Chart</span></a>
			<p class="widget-shortdesc"> Track performance over time.</p>
			<br>
			
			<p class="widget-list-item"><i class="material-icons meta-bullet red-text">stop</i><span class="red-text">type:</span> <span class="widget-author widget-meta">Visualisation</span></p>
			<p class="widget-list-item"><i class="material-icons meta-bullet green-text">stop</i><span class="green-text">tags:</span> <span class="widget-tags widget-meta">time-series,ranking</span></p>
			<p class="widget-list-item"><i class="material-icons meta-bullet blue-text">stop</i><span class="blue-text">libraries:</span> <span class="widget-jslibs widget-meta">ggplot2,ggflags</span>
			<span class="widget-release-nr">3</span>
		</p>
			<!-- <div class="more-icon activator"><i class="material-icons right">more_vert</i></div> -->
			<div class="hidden widget-cran">true</div>
		  </div>
		  <div class="card-reveal" style="display: none; -webkit-transform: translateY(0px);">
			<span class="card-title grey-text text-darken-4">Bump Chart<i class="material-icons right">close</i></span>
			<p>(full meta data to go here)</p>
			</div>
		</div>

	</div>
</div>