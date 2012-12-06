OXGAssetPicker
==============
It's ALAsset Picker For Titanium.  

![Albums](https://github.com/hiphapis/OXGAssetsPicker/blob/master/documentation/albums.png?raw=true)
![Photos](https://github.com/hiphapis/OXGAssetsPicker/blob/master/documentation/photos.png?raw=true)

You can show Album View & Photo View.  
Follow this code (from example/app.js)

	var win = Ti.UI.createWindow({});

	var albumWin = Ti.UI.createWindow({ title: "Albums" });
	var nav = Titanium.UI.iPhone.createNavigationGroup({ window: albumWin });
	win.add(nav);

	// TODO: write your module tests here
	var assetpicker = require('com.oxgcp.assetpicker');
	Ti.API.info("module is => " + assetpicker);

	var album = assetpicker.createAlbumView({
			top:0,
			left:0,
			width:Ti.UI.FILL,
			height:Ti.UI.FILL,
			backgroundColor:'white',
	});
	albumWin.add(album);
	album.addEventListener('album:selected', function(ae) {
			console.log(ae);

			var photoWin = Titanium.UI.createWindow({ title: ae.groupName });
			var photo = assetpicker.createPhotoView({
					groupName: ae.groupName, // load all photos If you remove property of groupName
					filter: "photo", // or "video", "all"
					top:0,
					left:0,
					width:320,
					height:460,
					backgroundColor:'white',
					multiple: true,
			});
			photoWin.add(photo);
			photo.addEventListener('photo:selected', function(pe) {
				console.log(pe);
			});
		
			nav.open(photoWin, { animated:true });
	});

	win.open();

Run Simulator  
`$ titanium run`  
Help: [Step 0: Setting Up your Module Environment](http://docs.appcelerator.com/titanium/latest/#!/guide/iOS_Module_Development_Guide-section-29004946_iOSModuleDevelopmentGuide-Step0%3ASettingUpyourModuleEnvironment)


If you want Packagin and Distribution Then read it.  
[Step 3: Packaging your Module for Distribution](http://docs.appcelerator.com/titanium/latest/#!/guide/iOS_Module_Development_Guide-section-29004946_iOSModuleDevelopmentGuide-Step3%3APackagingyourModuleforDistribution)