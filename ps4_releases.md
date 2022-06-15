<a id="releases-top"> </a>

# Releases

Each version of the SDK is hosted in a CDN to allow faster and more efficient developments. Optionally, the library can be downloaded and hosted on a custom server.

#### Version 1.2.5

```
https://nexplayer.nexplayersdk.com/NexHTML5/1.2.5_20211025/nexplayer.js
```

**Bug fixes:**
- Subtitles tracks were not being notified correctly when they were detected. Now, it is only necessary to listen to <a href="https://nexplayer.github.io/TizenWebOS/#/ps4_usage?id=player-events">"newsubtitlesdataloaded"</a>  event to be notified when a new subtitle is loaded.

Date: October 25th 2021

#### Version 1.2.4

**New features:**
- Implemented garbage collection for thumbnails in order to get rid of out of memory errors. Chunks that are out of the thumbnails loading range are removed from the loaded chunks array.

Date: September 23rd 2021

#### Version 1.2.3

**New features:**
- Added property "adsParamsToEncode" that must provide an Array of strings specifying the parameters in the ad URL to be encoded. For example: ["video_url_to_fetch"]
- Added new methods in order to fetch properties status (more info <a href="https://nexplayer.github.io/TizenWebOS/#/ps4_usage?id=getters-2">here</a>):

    * **getCurrentContentType()**: string → returns the the type of the current asset (“Ad”, “Main content” or “None”).
    * **getCurrentTime()**: number → returns the current time of the video.
    * **getPlaybackRate()**: number → returns the playback rate/speed of the video.
    * **getProtocol()**: NexProtocol  → returns the protocol of the stream used: 
    * **getVersion()**: string → returns the version of the SDK.
    * **isCurrentAssetAd()**: boolean → indicates whether the current asset playing is an ad or not; 
    * **isCurrentAssetMuted()**: boolean → returns whether the ad or the main content is muted or not.

- Added a new event, “bufferType”. this new event will be fired when a buffering event occurs and it specifies what type of buffering occurred ("Connection", "Seek", "Initial", "Background"). More info about events <a href="https://nexplayer.github.io/TizenWebOS/#/ps4_usage?id=playerevents">here</a>.

**Bug fixes:**
- Fixed non-resolving promises which lead to out of memory errors when fetching thumbnails

Date: August 10th 2021

#### Version 1.2.2

**Bug fixes:**
  - Renamed Frame object "canvas" property to "thumbnail".
  - Fixed permanent pending promise when fetching thumbnails that lead to "undefined" resolutions.

Date: July 30th 2021

#### Version 1.2.1

**Bug fixes:**
  - Fixed thumbails width and height properties as they were swapped.

Date: July 29th 2021

#### Version 1.2.0

New features:
  - Added SSAI support for PS4. It can be used through the property 'ssaiMediaTailor'.
  
    Property:
    * ssaiMediaTailor:
    {
      baseURL: string, //Base URL for Video and Ads
      playbackURL: string, //Video URL to be attached to the baseURL
      adsParams:
      {
        "param1": string, //Ad URL to be attached to the baseURL
      }
    }
    
  - Thumbnail enhancements. The method getThumbnailAt(time) now returns a promise instead of a
  thumbnail.
  
    * getThumbnailAt(time) // returns a Promise awaiting the corresponding thumbnail in a specific 
    time value

Date: July 23rd 2021

#### Version 1.1.9

**New features:**
  - Added New Relic support for PS4. It can be used through the property 'useNewRelicTracker'.
  A tracker library and agent must be included for this feature to work. Ask NexPlayer team for it.
  Custom data methods have also been added: 
  
    Property:
    * useNewRelicTracker: boolean, // true when enabling New Relic, false when not
    
    Methods:
    * addTrackerData(key: string, value: any) 
    * removeTrackerData(key: string, value: any)
  - Added milestone management for trailers and scrubbing. 
  A stream will be considered as a trailer when using the following property in the Setup:
    * trailer: boolean, // true when stream should be considered a trailer, false when not
  - 60 seconds in event added. When the video current time is at least 60 seconds, this 
  event gets triggered. This just happens once for each player instance. Usage:
    * addEventListener('60secondsin', function)
  - Added PS4 SDK protection using an external app ID.
  - Thumbnail enhancements. Vtts can now reference another Vtt inside them. 
  Two new methods for thumbnail retrieval have been added: 
    * getThumbnails() // returns the current loaded thubmnails
    * getThumbnailAt(time) // returns the corresponding thumbnail in a specific time value

Date: May 25th 2021

#### Version 1.1.8

**New features**:
  - Setup can be called prior to Unmount in order to reduce the delay when restarting
  the player. The configuration provided in the last Setup call is saved and will be 
  used to initialize the player as soon as Unmount ends.
  - CC style has been changed to use text shadows instead of a background colour.
  - Increased log interval when waiting for player to unmount and reduced the time until
  the player considers failure when destroying itself.

Date: April 20th 2021

#### Version 1.1.7

**New features**:
  - UnMount function has changed its return type. Now returns a Promise which is resolved when the player
  is the destroyed completely, as well as the method destroy of the player:
  
    * destroy(): Promise<any>;
    * export declare var UnMount: (div: HTMLDivElement) => Promise<any>;
    
  Check the <a href="https://nexplayer.github.io/TizenWebOS/#/ps4usage?id=unmount">API</a> for more info.

**Bug fixes:**
  - Seeking becomes broken after we destroy the player while 'seeking' previous content.
  - No cc on live streams for PS4.
  - Overlapping captions are shown multiple times when using WebVTT subtitles on VOD.

Date: March 30th 2021

#### Version 1.1.6

**New features:**
  - New player event "newsubtitlesdataloaded". It is fired when new text track are detected. Currently, embedded CC text track
  is detected later so this event can be fired several times. You should use this event for retrieving the current text tracks of the stream.
  - Added "stalled" event. It is fired when no more data is buffered and the player can't continue the playback.

**Bug fixes:**
  - Fixed issue regarding the delayed CC on VoD content.
  - Embedded CC cea 608/708 working on live streams.
  - Text missing when using embedded CC cea 608/708.
  - "seeked" event is working again.
  - Player's state "playing" is only reported when it is actually playing.

Date: March 18th 2021

#### Version 1.1.5

  - Added support for static and chunked thumbnails. Include the following property in Nexplayer's SetUp:
    > Static:
        thumbnails:
        {
            canvas: document.getElementById("canvas_id"),
            urlVtt: "url_string",
            urlImg: "url_string",
        }
        * canvas: HTML Canvas element where thumbnails will be displayed on.
        * urlVtt: Thumbnail VTT URL containing each thumbnail's time interval and coordinates.
        * urlImg: Thumbnail sprite URL containing multiple thumbnails stiched together.
    > Chunked:
        thumbnails:
        {
            canvas: document.getElementById("canvas_id"),
            urlVtt: "url_string",
            chunkLimit: 3,
            chunkTotal: 30,
        }
        * canvas: HTML Canvas element where thumbnails will be displayed on.
        * urlVtt: Thumbnail VTT URL containing each thumbnail's time interval and image URL.
        * chunkLimit (optional): Maximum number of thumbnail chunks to load at a time. Default: 1.
        * chunkTotal (optional): Total number of chunks to split the thumbnails' array into. Default: 1.

**Bug fixes:**
  - Improved algorithm that filters the subtitles cues which removes the delay observed
  on the subtitles shown.

Date: March 9th 2021

#### Version 1.1.4

**New features:**
  - Added property "detail" into the events objects for offering backwards compatibility with the legacy SDK.

Date: March 4th 2021

#### Version 1.1.3

**New features:**
  - New events regarding the progression of the video:
    - "videofirstquartile": fired when the video reaches the point 25% of the total duration.
    - "videomidpoint": fired when the video reaches the point 50% of the total duration.
    - "videothirdquartile": fired when the video reaches the point 75% of the total duration.
  - All of these events will contain the property "quartileTime" in the property "_data" of the event received:

```js
    nexplayer.PlayerEvents("videofirstquartile", function (e) {
      console.log(" VIDEO FIRST QUARTILE --------------------", e._data.quartileTime);
    });
```

Date: February 26th 2021

#### Version 1.1.2

- Official release containing all the features and bug fixes from the previous versions.

Date: February 23rd 2021

#### Version 1.1.1

**Bug fixes:**
- Fixed state issue.

Date: February 18th 2021

#### Version 1.1.0

**Bug fixes:**
  - DURATION_CHANGE event is triggered when the duration of the stream
  is retrieved. The event will contain the duration of the video.
  - getCurrentSubtitle() method now returns a number. It represents the index of the
  current activated subtitle, -1 if no subtitle is activated.
  - BUFFERING event is triggered when player changes to buffering state.
  - videometrics object related error shouldn't be appearing. We can't confirm
  as we couldn't reproduce it even once.

**New features:**
  - SEEKING event added. It is triggered when the player starts seeking.
  - SEEKED event added. It is triggered when the player finishes seeking.
  - isSeeking() method. It returns a boolean indicating if the player
  is currently seeking.
  - New volume methods are implemented for the player and the adsManager:
  setVolume(value:number), getVolume():number,
  setMute(mute:boolean) and getMute(): boolean.

Date: February 17th 2021