# Wakeup / Alarm Clock PhoneGap / Cordova Plugin

### Platform Support

This plugin supports PhoneGap/Cordova apps running on both iOS and Android.

### Version Requirements

This plugin is meant to work with Cordova 3.5.0+.

## Installation

#### Automatic Installation using PhoneGap/Cordova CLI (iOS and Android)
1. Make sure you update your projects to Cordova iOS version 3.5.0+ before installing this plugin.

	cordova platform update ios
	cordova platform update android

2. Install this plugin using PhoneGap/Cordova cli:

	cordova plugin add https://github.com/uiwise/cordova-plugin-wakeuptimer.git

## Usage

	// All responses from the audio player are channeled through successCallback and errorCallback

	// Set wakeup timer
	window.wakeuptimer.wakeup(successCallback, errorCallback, {
		alarms : [{
			type: "onetime",
			time: {hour : 14, minute : 30},
			extra: {message : "JSON containing app-specific information to be posted when alarm triggers"},
			message: "Alarm has expired!"
		}]
	});

	// Snooze...
	window.wakeuptimer.snooze(successCallback, errorCallback, {
		alarms : [{
			type: "snooze",
			time: {seconds : 60}, // Snooze for 60 seconds 
			extra: {}, // JSON containing app-specific information to be posted when alarm triggers
			message: this.get("message"),
			sound: this.get("sound"),
			action: this.get("action")
		}]
	});

	// Example of a callback method
	var successCallback = function(result) {
		if(result.type === "wakeup") {
			console.log("wakeup alarm detected: " + result.extra);
		} else if(result.type === "set") {
			console.log("wakeup alarm set: " + result);
		} else {
			console.log("wakeup unhandled type (" + result.type + ")");
		}
	};
