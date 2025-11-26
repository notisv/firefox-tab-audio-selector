# firefox-tab-audio-selector
Firefox bookmarklet to select audio output device for each tab. Tested on Firefox v145.

## Bookmarklet setup
Create a bookmark, name it appropriately, and paste the following code into the url section.<br>
Pin it to your toolbar for easy access.

```
javascript:(async()=>{const mediaElements=document.querySelectorAll("audio,video");if(!mediaElements.length){alert("No audio or video elements found on this page.");return}if(typeof mediaElements[0].setSinkId!=="function"){alert("The browser does not support audio output switching.\nIn Firefox, enable it by:\n1. Opening about:config\n2. Settingmedia.setsinkid.enabled = true");return}try{const deviceId=await navigator.mediaDevices.selectAudioOutput();mediaElements.forEach(elem=>elem.setSinkId(deviceId.deviceId))}catch(err){console.log(err)}})();
```

The code in an easily readable format:
```
javascript:(async () => {
    const mediaElements = document.querySelectorAll("audio, video");

    if (!mediaElements.length) {
        alert("No audio or video elements found on this page.");
        return;
    }

    if (typeof mediaElements[0].setSinkId !== "function") {
        alert(
            "The browser does not support audio output switching.\n" +
            "In Firefox, enable it by:\n" +
            "1. Opening about:config\n" +
            "2. Setting media.setsinkid.enabled = true"
        );
        return;
    }

    try {
        const deviceId = await navigator.mediaDevices.selectAudioOutput();
        mediaElements.forEach(elem => elem.setSinkId(deviceId.deviceId));
    } catch (err) {
        console.log(err);
    }
})();
```

## Usage
Click the bookmark on any tab you want to change the audio output device.<br>
When navigating to another webpage, the output device is reset and needs to be changed again.<br>
Keep in mind that the audio output device cannot be changed when actively using FFZ Audio Compressor on Twitch.

## License
This code is available under the MIT License.
