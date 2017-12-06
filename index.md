---
layout: default
---
<script src="https://code.jquery.com/jquery-1.10.2.js"></script>
<script type="text/javascript">

	// load meta data fron json file
	$.getJSON( "meta.json", function( data ) {
	  
	  var releaseElement = $("#releases-dox-list");
	  var releaseFound = false;
	  
	  // get releases
	  if (data.hasOwnProperty("releases")) {
	    
	    var releases = data.releases;
	    var keys = Object.keys(releases);
	    
	    for(var rel in keys) {
	      
	      var relTitle = $("<h3>");
	      relTitle.html("DQM4hep (" + String(keys[rel]) + ")");
	      relTitle.appendTo( releaseElement );
	      
	      var pkgs = releases[keys[rel]];
	      var pkgKeys = Object.keys(pkgs);
	      pkgListElement = $("<ul>");
	      pkgListElement.appendTo(releaseElement);
	      
	      for(var pkg in pkgKeys) {
	        
	        pkgName = pkgKeys[pkg];
	        pkgVersion = pkgs[pkgName];
	        
	        pkgElement = $("<li>");
	        pkgAnchor = $("<a>");
	        pkgAnchor.attr("href", "/doxygen/" + pkgName + "/" + pkgVersion + "/index.html");
	        pkgAnchor.append(pkgName);
	        pkgAnchor.appendTo(pkgElement); 
	        pkgElement.append(" (" + pkgVersion + ")");
	                   
	        pkgElement.appendTo(pkgListElement);
	      }
	      
	      releaseFound = true;
	    }
	  }
	  
	  if ( ! releaseFound ) {
	    
	    var text = $("<p>");
	    text.html("No release yet. Read the master documentation of the different packages");
	    text.appendTo( releaseElement );
	    
	    console.log( "no release found !" );
	  }
	  
	  
	  
	  var packagesElement = $("#packages-dox-list");
	  
	  // get packages documentation
	  if (data.hasOwnProperty("packages")) {
	    
	    var packages = data.packages;
	    var keys = Object.keys(packages);
	    
	    for(var index in keys) {
	      
	      var pkgName = keys[index];
	      var pkgVersions = packages[pkgName].versions;
	                        
	      var pkgTitle = $("<h3>");

	      pkgTitle.html(pkgName);
	      pkgTitle.appendTo(packagesElement);
	      
	      versionListElement = $("<ul>");
	      versionListElement.appendTo(packagesElement);
	      
	      for (var v in pkgVersions) {
	        
	        var version = pkgVersions[v];
	        console.log("Package: " + pkgName + ", version: " + version);
	        
	        versionElement = $("<li>");
	        
	        if (version == "master") {
	          versionElement.prependTo(versionListElement);              
	        }
	        else {
	          versionElement.appendTo(versionListElement);
	        }

	        versionAnchor = $("<a>");
	        versionAnchor.attr("href", "/doxygen/" + pkgName + "/" + version + "/index.html");
	        versionAnchor.html(version);
	        versionAnchor.appendTo(versionElement);
	      }
	    }
	  }
	  
	});
    

</script>

<div id="main_content_wrap" class="outer">
	<section id="main_content" class="inner">

		<h1> DQM4hep doxygen documentation hosting </h1>

<p>This page collect the doxygen pages for the different packages of DQM4hep.</p>
<p>Not all packages build a doxygen documentation, as some of them are external and can be referenced from some other webpages.</p>
<br/>
<p>You might also want to read our user manual or related "less-technical" documentation.</p>
<p>You can find it here : <a href="http://dqm4hep.readthedocs.io">http://dqm4hep.readthedocs.io</a></p>

<div class="dox-section">
  <h2> External packages documentation </h2>
  <ul>
      <li> <a href="http://dim.web.cern.ch/dim/cpp_doc/DimCpp.html"> DIM cpp documentation </a> </li>
      <li> <a href="http://jsoncpp.sourceforge.net/annotated.html"> jsoncpp doxygen documentation </a> </li>
  </ul>
</div>

<div class="dox-section">
  <h2> DQM4hep releases documentation </h2>
  <div id="releases-dox-list" />
</div>

<div class="dox-section">
  <h2> DQM4hep packages documentation </h2>
  <div id="packages-dox-list" />
</div>

	</section>
</div>