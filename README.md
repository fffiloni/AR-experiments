# AR-experiments

### Working with AR.js and A-Frame

```html
<script src="https://aframe.io/releases/0.8.0/aframe.min.js"></script>
<script src="https://jeromeetienne.github.io/AR.js/aframe/build/aframe-ar.js"></script>
<script>THREEx.ArToolkitContext.baseURL = "https://rawgit.com/jeromeetienne/ar.js/master/three.js/"</script>
```


### Working with AR.js and Three.js

```html
//three.js library
<script src="https://cdn.rawgit.com/jeromeetienne/AR.js/0694b414/three.js/examples/vendor/three.js/build/three.min.js"></script>
<script src="https://cdn.rawgit.com/jeromeetienne/AR.js/0694b414/three.js/examples/vendor/three.js/examples/js/libs/stats.min.js"></script>
//ar.js
<script src="https://cdn.rawgit.com/jeromeetienne/AR.js/0694b414/three.js/build/ar.js"></script>
<script>
  THREEx.ArToolkitContext.baseURL = "https://github.com/jeromeetienne/AR.js/tree/master/three.js/";
</script>
```

### Add Event listener on markers

```html
<a-scene>
  <a-marker preset="hiro" markerhandler emitevents="true" id="hiroMarker">

    // Your entities

  </a-marker>
</a-scene>


// Before body close tag

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
