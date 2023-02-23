# zuck.js

[![Zuck.JS demo](https://raw.githubusercontent.com/ramon82/assets/master/zuck.js/preview.gif)](https://on.ramon82.com/2k9e7au)

## Add stories EVERYWHERE
MWHAHAHAHA. Seriously. This script is a copy of Facebook Stories of ~~a copy of Facebook Messenger Day (RIP)~~ of a copy of WhatsApp status of a copy of Instagram stories of a copy of Snapchat stories. 

You can read stories from any endpoint (JSON, Firebase, etc.) and the script will do the rest.

Live demo: https://on.ramon82.com/2k9e7au

React sample: https://on.ramon82.com/2lDP53H

[![CDNJS](https://img.shields.io/cdnjs/v/zuck.js.svg?colorA=333333&colorB=D32F2F&style=flat-square&maxAge=3600)](https://cdnjs.com/libraries/zuck.js) [![NPM](https://img.shields.io/npm/v/zuck.js.svg?colorA=333333&colorB=D32F2F&style=flat-square&maxAge=3600)](https://www.npmjs.com/package/zuck.js)


## Features
* Custom CSS themes: [Snapgram](https://rawgit.com/ramon82/zuck.js/master/index.html?skin=Snapgram), [FaceSnap](https://rawgit.com/ramon82/zuck.js/master/index.html?skin=FaceSnap), [Snapssenger](https://rawgit.com/ramon82/zuck.js/master/index.html?skin=Snapssenger) and [VemDeZAP](https://rawgit.com/ramon82/zuck.js/master/index.html?skin=VemDeZAP)
* Gestures, Custom events & custom templates
* A simple API to manage your "Stories timeline"
* 3D cube effect
* React support
* RTL support


## How to use
You can download this git repository or install via ```npm install zuck.js```

Initialize:

```js
let element = document.querySelector("#stories");
let stories = Zuck(element, {
  skin: 'snapgram',      // container class
  avatars: true,         // shows user photo instead of last story item preview
  list: false,           // displays a timeline instead of carousel
  openEffect: true,      // enables effect when opening story
  cubeEffect: false,     // enables the 3d cube effect when sliding story
  autoFullScreen: false, // enables fullscreen on mobile browsers
  backButton: true,      // adds a back button to close the story viewer
  backNative: false,     // uses window history to enable back button on browsers/android
  previousTap: true,     // use 1/3 of the screen to navigate to previous item when tap the story
  localStorage: true,    // set true to save "seen" position. Element must have a id to save properly.
  reactive: true,        // set true if you use frameworks like React to control the timeline (see react.sample.html)
  rtl: false,            // enable/disable RTL

  stories: [ // array of stories
    // see stories structure example
  ],

  callbacks:  {
    onOpen (storyId, callback) {
      callback();  // on open story viewer
    },

    onView (storyId) {
      // on view story
    },

    onEnd (storyId, callback) {
      callback();  // on end story
    },

    onClose (storyId, callback) {
      callback();  // on close story viewer
    },

    onNavigateItem (storyId, nextStoryId, callback) {
      callback();  // on navigate item of story
    },

    onDataUpdate (currentState, callback) {
      callback(); // use to update state on your reactive framework
    }
  },

  template: {
    // use these functions to render custom templates
    // see src/zuck.js for more details

    timelineItem (itemData) {
      return ``;
    },

    timelineStoryItem (itemData) {
      return ``;
    },

    viewerItem (storyData, currentStoryItem) {
      return ``;
    },

    viewerItemPointer (index, currentIndex, item) {
      return ``;
    },

    viewerItemBody (index, currentIndex, item) {
      return ``;
    }
  },

  language: { // if you need to translate :)
    unmute: 'Touch to unmute',
    keyboardTip: 'Press space to see next',
    visitLink: 'Visit link',
    time: {
      ago:'ago', 
      hour:'hour', 
      hours:'hours', 
      minute:'minute', 
      minutes:'minutes', 
      fromnow: 'from now', 
      seconds:'seconds', 
      yesterday: 'yesterday', 
      tomorrow: 'tomorrow', 
      days:'days'
    }
  }
});
```

Add/update a story (timeline item):

```js   
stories.update({item object});
 ```

Remove a story:

```js
stories.remove(storyId); // story id
```

Add/remove a story item:

```js
stories.addItem(storyId, {item object});
stories.removeItem(storyId, itemId);
```


### Stories structure example
See `StoriesTimeline` on `./types.ts`


### Alternate call
In your HTML:

```HTML
<div id="stories">

    <!-- story -->
    <div class="story {{ story.seen ? 'seen' : '' }}" data-id="{{storyId}}" data-last-updated="{{story.lastUpdated}}" data-photo="{{story.photo}}">
        <a class="item-link" href="{{story.link}}">
          <span class="item-preview">
            <img src="{{story.photo}}" />
          </span>
          <span class="info" itemProp="author" itemScope="" itemType="http://schema.org/Person">
            <strong class="name" itemProp="name">{{story.name}}</strong>
            <span class="time">{{story.lastUpdated}}</span>
          </span>
        </a>
        
        <ul class="items">
        
            <!-- story item -->
            <li data-id="{{storyItemId}}" data-time="{{storyItem.time}}" class="{{storyItem.seen}}">
                <a href="{{storyItem.src}}"
                
                 data-type="{{storyItem.type}}" 
                 data-length="{{storyItem.length}}" 
                 data-link="{{storyItem.link}}" 
                 data-linkText="{{storyItem.linkText}}" 
                 
                 data-custom-key="{{storyItem.custom-key}}" 
                 data-another-custom-key="{{storyItem.another-custom-key}}">
                    <img src="{{storyItem.preview}}" />
                </a>
            </li>
            <!--/ story item -->
            
        </ul>
    </div>
    <!--/ story -->
    
</div>
```
    
Then in your JS:

```js
let stories = Zuck(element); 
```


### Tips
- You can use with autoFullScreen option (disabled by default) to emulate an app on mobile devices.
- If you use Ionic or some js that uses ```location.hash```, you should always disable the "backNative" option which can mess your navigation.


## Limitations
On mobile browsers, video can't play with audio without a user gesture. So the script tries to play audio only when the user clicks to see the next story. 
When the story is playing automatically, the video is muted, but an alert is displayed so the user may click to turn the audio on.

Stories links opens in a new window too. This behaviour occurs because most websites are blocked on iframe embedding. 


## License
MIT


## Show your support!
Please ⭐️ this repository if this project helped you! Feel free to buy me a coffee:

[![ko-fi](https://www.ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/F1F710G8L)
