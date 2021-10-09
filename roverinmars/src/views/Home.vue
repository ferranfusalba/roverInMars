<template>
  <div class="text-white">
    <div>
    <h1>Welcome to RoverInMars</h1>
    <br />
    <h3>
        You have the opportunity now to move a rover in the surface on Mars
    </h3>
    <br>
    <h3>On the next page, you'll be asked to introduce a set of commands, such as:</h3>
    <h5>The dimensions of the square</h5>
    <h5>The coordinates in which the rover will start moving</h5>
    <h5>The initial orientation</h5>
    <h5>
      The three allowed commands: Advance (A), Turn Left (L), Turn Right (R)
    </h5>
    <br>
    <h3>Please, hit next to continue</h3>
    <router-link to="/next" class="tdn text-white"><button class="btn btn-lg btn-primary">Next</button></router-link>
  </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  
}
</script>