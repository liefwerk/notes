# dynamic_css

We can  change the classes dynamicaly.

```
<div class="" :class="{available: available}"></div>

new Vue({
    // targets <div class="" id="vue-app"></div>
    el: '#vue-app',
    data: {
        available: false,
        nearby: false
    },
    methods: {},
    computed: {}
});
```

We could also pass the classes as an object from a function into the div
```

computed: {
    // the classes are passed as an object here
    compClasses: function(){
        return {
            available: this.available,
            nearby: this.nearby
        }
    }
}

// we add an event on click with @click to change the boolean variables nearby and available
<button @click="nearby = !nearby">Toggle nearby</button>
<button @click="available = !available">Toggle available</button>

// here we add the classes as an object
<div :class="compClasses">

<span>Ryu</span>

</div>
```
