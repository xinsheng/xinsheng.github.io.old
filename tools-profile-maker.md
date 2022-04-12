---
layout: page
title: AirPrint profile maker
---

Make airprint profile in case you cannot find specific printer in LAN.

<script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
<fieldset id="forms__input">
  <legend>Input fields</legend>
  <p>
	<label>Printer IP Address</label>
	<input id="ip" type="text" placeholder="192.168.1.1" />
  </p>
  <p>
	<label>Resource Path</label>
	<input
	  id="path"
	  type="text"
	  value='ipp/print'
	/>
  </p>
  <input type="button" onclick="build()" value="Download Profile" />
</fieldset>
<script>
const downloadBlobAsFile = function(data, filename){
	const contentType = 'application/x-apple-aspen-config';
	if(!data) {
		console.error('No data')
		return;
	}
	if(typeof data === "object"){
		data = JSON.stringify(data, undefined, 4)
	}

	var blob = new Blob([data], {type: contentType}),
		e    = document.createEvent('MouseEvents'),
		a    = document.createElement('a')

	a.download = filename
	a.href = window.URL.createObjectURL(blob)
	a.dataset.downloadurl =  [contentType, a.download, a.href].join(':')
	e.initMouseEvent('click', true, false, window, 0, 0, 0, 0, 0, false, false, false, false, 0, null)
	a.dispatchEvent(e)
}
	
function build(){
	ip = $('#ip').val();
	path = $('#path').val();
	if(!ip){
		alert("Printer IP Address is empty!");
		return;
	}
	var profile = `<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>PayloadContent</key>
	<array>
		<dict>
			<key>AirPrint</key>
			<array>
				<dict>
					<key>IPAddress</key>
					<string>`+ip+`</string>
					<key>Port</key>
					<integer>631</integer>
					<key>ResourcePath</key>
					<string>`+path+`</string>
				</dict>
			</array>
			<key>PayloadDisplayName</key>
			<string>AirPrint</string>
			<key>PayloadIdentifier</key>
			<string>com.apple.airprint.E9A15E0B-2FD5-47EF-90D5-D6BECDE86AD8</string>
			<key>PayloadType</key>
			<string>com.apple.airprint</string>
			<key>PayloadUUID</key>
			<string>E9A15E0B-2FD5-47EF-90D5-D6BECDE86AD8</string>
			<key>PayloadVersion</key>
			<integer>1</integer>
		</dict>
	</array>
	<key>PayloadDisplayName</key>
	<string>`+ip+`</string>
	<key>PayloadIdentifier</key>
	<string>D9558BA5-A48A-4A5B-B2B5-A8BBC9C884E8</string>
	<key>PayloadRemovalDisallowed</key>
	<false/>
	<key>PayloadType</key>
	<string>Configuration</string>
	<key>PayloadUUID</key>
	<string>4F465CDC-C108-476E-A447-92DDCA6B5BD8</string>
	<key>PayloadVersion</key>
	<integer>1</integer>
</dict>
</plist>`
    downloadBlobAsFile(profile, "airprint.mobileconfig");
}
</script>