# AR-experiments

### Working with AR.js and A-Frame

```html
<script src="https://aframe.io/releases/0.8.0/aframe.min.js"></script>
<script src="https://jeromeetienne.github.io/AR.js/aframe/build/aframe-ar.js"></script>
<script>THREEx.ArToolkitContext.baseURL = "https://rawgit.com/jeromeetienne/ar.js/master/three.js/"</script>
```


### Working with AR.js and Three.js

```html
<!--three.js library-->
<script src="https://cdn.rawgit.com/jeromeetienne/AR.js/0694b414/three.js/examples/vendor/three.js/build/three.min.js"></script>
<script src="https://cdn.rawgit.com/jeromeetienne/AR.js/0694b414/three.js/examples/vendor/three.js/examples/js/libs/stats.min.js"></script>

<!--ar.js-->
<script src="https://cdn.rawgit.com/jeromeetienne/AR.js/0694b414/three.js/build/ar.js"></script>
<script>
  THREEx.ArToolkitContext.baseURL = "https://github.com/jeromeetienne/AR.js/tree/master/three.js/";
</script>
```

### Generate your own markers

To generate your own custom markers, you can use [this generator](https://jeromeetienne.github.io/AR.js/three.js/examples/marker-training/examples/generator.html), made by Jérôme Etienne.

#### Prerequisites

To create an efficient marker, you need to be careful of the following steps:
*   white part of your marker should be set to a light-grey color, like #ddd for example. This will help the tracking, also remember that paper is not fully white in real life.
*   if you want to use a custom icon, or picture, make sure it is bold enough, then put it in a corner. This will also help the tracking, telling the camera where are  the up, the bottom, the left and the right sides.

#### Using your custom markers

Put your .patt on your server, then call it in your index.html file like this:
```html
<a-marker preset="custom" type="pattern" url="path/to/your-marker.patt">

  <a-entity>
  </a-entity>

</a-marker>
```

Repeat this block for each entity that you want to use a specific marker with.

#### Using a QR-Code to get the adress of your web AR app

To generate a Hiro Code containing a QR-Code, you can use [this generator](https://jeromeetienne.github.io/AR.js/three.js/examples/arcode.html), provided by Jérôme Etienne.

### Add Event listener on markers

```html
<a-scene>
  <a-marker preset="hiro" markerhandler emitevents="true" id="hiroMarker">

    <!-- Your a-frame entities-->

  </a-marker>
</a-scene>


<!-- Before body close tag -->

<script>
  AFRAME.registerComponent('markerhandler', {
      init: function() {
        // Set up the tick throttling. Will check if marker is active every 500ms
        this.tick = AFRAME.utils.throttleTick(this.tick, 500, this);
      },
      tick: function(t, dt) {
        if (document.querySelector("#hiroMarker").object3D.visible == true) {
          // MARKER IS PRESENT
          //alert("MARKER IS PRESENT")
          console.log("marker is present");

        } else {
          // MARKER IS HIDDEN, do nothing (up to you)
          //onsole.log("marker is not present");
        }
      }
    }
  );
</script>
```

### Fix to make videos working properly on mobile

Your video asset must be serve from the same domain if you want to play it on iOS

-   Add `<meta name="apple-mobile-web-app-capable" content="yes">` in HEAD
-   Your video asset needs this attribute: webkit-playsinline
`<video id="video" src="videos/video.mp4" muted webkit-playsinline autoplay loop></video>`
-   Add this before the body end tag:
```html
<script type="text/javascript">
function togglePlayback () {
  var el = document.getElementById('video') // or vid ?
  var material = Object.assign({}, el.getAttribute('material'))
  material.pause = !material.pause
  el.setAttribute('material', material)
}
</script>

```

### Important Notice

Don't forget to serve your files from a HTTPS secure connection, then it should work properly on iOS Safari.

### Credits

Some templates borrow works from Jérôme Etienne, Mayognaise, Lee Stemkoski.
Some 3D models come from poly.google.com
