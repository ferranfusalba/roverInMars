<template>
  <div id="app">
    <div class="row">
      <div class="col-3">
        <h2>Set commands</h2>
        <div class="row">
          <form>
            <div class="row">
              <div class="mt-4 mb-4">
                <h4>Grid size</h4>
                <div class="row">
                  <div class="col-6">
                    <label>Width</label>
                    <input
                      type="number"
                      class="form-control"
                      min="0"
                      v-model="gridWidth"
                    />
                  </div>
                  <div class="col-6">
                    <label>Height</label>
                    <input
                      type="number"
                      class="form-control"
                      min="0"
                      v-model="gridHeight"
                    />
                  </div>
                </div>
              </div>
              <div class="mt-4 mb-4">
                <h4>Initial coordinates</h4>
                <div class="row">
                  <div class="col-6">
                    <label>X</label>
                    <input
                      type="number"
                      class="form-control"
                      v-model="initialX"
                    />
                  </div>
                  <div class="col-6">
                    <label>Y</label>
                    <input
                      type="number"
                      class="form-control"
                      v-model="initialY"
                    />
                  </div>
                </div>
              </div>
              <div class="mt-4 mb-4">
                <h4>Initial orientation</h4>
                <!-- North -->
                <div class="form-check form-check-inline">
                  <input
                    class="form-check-input"
                    type="radio"
                    id="roverOrientationNorth"
                    v-model="initialOrientation"
                    value="N"
                  />
                  <label class="form-check-label" for="roverOrientationNorth">
                    North
                  </label>
                </div>
                <!-- East -->
                <div class="form-check form-check-inline">
                  <input
                    class="form-check-input"
                    type="radio"
                    id="roverOrientationEast"
                    v-model="initialOrientation"
                    value="E"
                  />
                  <label class="form-check-label" for="roverOrientationEast">
                    East
                  </label>
                </div>
                <!-- South -->
                <div class="form-check form-check-inline">
                  <input
                    class="form-check-input"
                    type="radio"
                    id="roverOrientationSouth"
                    v-model="initialOrientation"
                    value="S"
                  />
                  <label class="form-check-label" for="roverOrientationSouth">
                    South
                  </label>
                </div>
                <!-- West -->
                <div class="form-check form-check-inline">
                  <input
                    class="form-check-input"
                    type="radio"
                    id="roverOrientationWest"
                    v-model="initialOrientation"
                    value="W"
                  />
                  <label class="form-check-label" for="roverOrientationWest">
                    West
                  </label>
                </div>
              </div>
              <div class="mt-4 mb-4">
                <h4>Select commands</h4>
                <input
                  type="text"
                  class="form-control"
                  readonly="readonly"
                  id="selectedCommands"
                  placeholder="Selected commands will be shown here"
                  v-model="commandSequence"
                />
                <div
                  class="mt-4 mb-4 btn-group"
                  role="group"
                  aria-label="Basic mixed styles example"
                >
                  <button
                    type="button"
                    class="btn btn-secondary"
                    @click="addCommandToSequence('L')"
                  >
                    Left
                  </button>
                  <button
                    type="button"
                    class="btn btn-primary"
                    @click="addCommandToSequence('A')"
                  >
                    Advance
                  </button>
                  <button
                    type="button"
                    class="btn btn-secondary"
                    @click="addCommandToSequence('R')"
                  >
                    Right
                  </button>
                </div>
                <div>
                  <button class="btn btn-danger" @click="clearCommandSequence">
                    Clear All Commands
                  </button>
                </div>
                <div class="mt-4">
                  <button
                    class="btn btn-lg btn-success"
                    @click="runRoverInMars"
                  >
                    RUN ROVER IN MARS
                  </button>
                </div>
              </div>
            </div>
          </form>
        </div>
      </div>
      <div class="col-9">
        <h2>Results from Mars</h2>
        <div v-if="roverResult == true" class="bg-success">
          The introduced commands return TRUE <br />
          They are placed inside the limits. <br />
          <b>Initial position:</b> <br />
          X Value: {{ initialValuesArray[0] }} <br />
          Y Value: {{ initialValuesArray[1] }} <br />
          Orientation: {{ initialValuesArray[2] }} <br />
          <b>End position:</b> <br />
          X Value: {{ initialX }} <br />
          Y Value: {{ initialY }} <br />
          Orientation: {{ initialOrientation }}
        </div>
        <div v-else-if="roverResult == false" class="bg-danger">
          The introduced commands return FALSE. <br />
          They are placed outside the limits.
        </div>
      </div>
    </div>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 10px;
  background-color: rgb(211, 109, 81);
}
</style>

<script>
//It´s needed a program to validate instructions that will be used by a new Rover in Mars
//Each Rover are included in a square and can receive the next commands: Advance (A), Turn left (L), Turn Right (R).
//The program must validate that the Rover be included into the edges of the square and must indicate the final orientation. (N, S, E, W)
//The program will receive the dimensions of the square (width x height) and it assumes that the coordinate (0,0) is the bottom left corner
//Additionally, will receive initial coordinates of the Rover and it’s initial orientation (N, S, E, W).
//Also it will receive a set of commands like the next one; “AALAARALA”.
//There is not fixed limit of number of input commands
//It can be assumed that there is not obstacles into the square.
//The program must validate that all the commands can be executed without be out of pre-defined initial limits and also must return True or False indicating if the commands are valid.Rover
//Moreover, also must return the orientation and final coordinates of the Rover
//
//The source code for this test will be sent as a different file GITHUB LINK with everything needed to run the solution and get the proper results.
//You can use any framework to build this although Angular or VueJS with Typescript is preferred.  VUE DOESN'T NEED TO USE TYPESCRIPT
//The solution must run with a single npm command.
//Angular with Typescript, Vue with Vanilla
//This test will be used to check technical skills into the recruiting process so consider all aspects you use to use every day to keep quality and architecture and everything else that define you as the good professional you are.
//Be honest with the time you invest to complete the whole test.





export default {
  name: "App",
  data() {
    return {
      commandSequence: "", //Seqüència de commands (L, A, R)
      commandSequenceArray: [], //Seqüència de commands (L, A, R) en Array
      roverOrientationArrayRight: ["N", "E", "S", "W"], //Opcions orientació Rover ordenades per 90º sentit horari
      gridWidth: 1, //Amplada width - 1 per defecte
      gridHeight: 1, //Alçada height - 1 per defecte
      initialX: 0, //Coordenada X - 0 per defecte
      initialY: 0, //Coordenada Y - 0 per defecte
      initialOrientation: "", //Orientation has no default value
      initialValuesArray: [], //Array dels valors inicials (x, y i orientació)
      numberOfCommands: 0, //Número de commands introduïts al 'Select commands' input
      roverResult: Boolean, //Boolean que depenent del resultat mostrarà un missatge true (amb coordenades) o false: no s'ha pogut validar.
    };
  },
  methods: {
    addCommandToSequence(command) {
      //Adds L, A or R commands to a String and to an Array at the same time
      //Es crida des dels botons "Left", "Advance" i "Right"
      this.commandSequence += command;
      this.commandSequenceArray.push(command);
    },
    clearCommandSequence() {
      //Clears both the Array and the String
      //Es crida des del botó "Clear all commands"
      this.commandSequence = "";
      this.commandSequenceArray = [];
    },
    runRoverInMars() {
      //Mètode general de validació (checkGeneral + checkInputsAndLimits);
      //Es crida des del botó "Run Rover In Mars"
      this.initialValuesArray.push(this.initialX); //Afegim valors inicials a l'Array per a mostrar-los després en pantalla (i comparar-los amb el final)
      this.initialValuesArray.push(this.initialY);
      this.initialValuesArray.push(this.initialOrientation);
      console.log(this.initialValuesArray);
      this.checkGeneral(); //ho validem tot
    },
    checkInputsAndLimits() {
      //Check that all inputs are not empty, and that they have a valid value
      if (this.initialX < 0) { //Comprova que no es puguin posar nombres negatius
        alert("Please, put a value for X above 0.");
        return false;
      } else if (this.initialY < 0) { //Comprova que no es puguin posar nombres negatius
        alert("Please, put a value for Y above 0.");
        return false;
      } else if (this.initialOrientation == "") {
        alert("Please, select the rover's initial orientation.");
        return false;
      } else if (this.commandSequence == "") {
        alert("Please, select at least a command for the rover.");
        return false;
      } else {
        //Comprovar que la X, Y i les mesures grid són iguals o superiors a 0 (igualment, X o Y inferiors ja no hagués deixat)
        //Mètode per retornar finalment true
        if (
          //this.gridWidth &&
          //this.gridHeight &&
          //this.initialX &&
          //this.initialY >= 0
          //this.gridWidth >= this.initialX && this.gridHeight >= this.initialY
          //Comprova que la diferència sigui sempre igual o superior a 0 perquè no pugui validar correctament una coordenada fora de la grid - els condicionals anteriorment comentats no funcionen igual
          this.gridWidth - this.initialX >= 0 && this.gridHeight - this.initialY >= 0
        ) {
          console.log("true");
          return true;
        } else {
          console.log("false");
          return false;
        }
      }
    },
    checkGeneral() {
      if (this.checkInputsAndLimits()) {
        //Es crida a la funció (no s'ha pogut retornar el true del Boolean)
        //Check que retorni true (tots els camps són amb dades i aquestes són vàlides, és a dir, dins la grid)
        if (this.numberOfCommands < this.commandSequenceArray.length) {
          //si 0 (inicialment) < la longitud del total de commands (per això hem creat l'Array)
          for (let i = 0; i < this.commandSequenceArray.length; i++) {
            var command = this.commandSequenceArray[this.numberOfCommands]; //Command introduït i a l'array
          }
          let orientationFinal = this.roverOrientationArrayRight.indexOf(
            //Cerca que algun índex de les 4 orientacions disponibles sigui el seleccionat
            this.initialOrientation
          );
          //No dóna el mateix resultat amb for o includes (Retorna Boolean)
          /*
      for (let i = 0; i < this.roverOrientationArrayRight.length; i++) {
        var orientationFinal = (this.roverOrientationArrayRight[i] = this.initialOrientation);
      } */
          //let orientationFinal = this.roverOrientationArrayRight.includes(this.initialOrientation);
          switch (command) {
            case "L": //Cas especial per anar al final de l'Array
              if (this.initialOrientation == "N") {
                this.initialOrientation = "W";
              } else {
                //Cas normal de girar 90º a l'esquerra, anant 1 element de l'array a l'esquerra
                this.initialOrientation =
                  this.roverOrientationArrayRight[orientationFinal - 1];
              }
              break;
            case "R": //Cas especial per anar a l'inici de l'Array
              if (this.initialOrientation == "W") {
                this.initialOrientation = "N";
              } else {
                //Cas normal de girar 90º a la dreta, anant 1 element de l'array a la dreta
                this.initialOrientation =
                  this.roverOrientationArrayRight[orientationFinal + 1];
              }
              break;
            case "A": //Cas especial per a l'Advance, al ser diferent que L i R
              if (this.initialOrientation == "N") {
                this.initialY += 1; //Actualitza el valor de initialY a la nova orientació, agafant la dada de dins l'Array (millor '+=' que '+')
              } else if (this.initialOrientation == "E") {
                this.initialX += 1;
              } else if (this.initialOrientation == "S") {
                this.initialY -= 1;
              } else if (this.initialOrientation == "W") {
                this.initialX -= 1;
              }
          }
          this.numberOfCommands++; //El numberOfCommands és inicialment 0, fins arribar al total de commands introduïts (anirà sumant i sevirà per controlar l'if que comprova que sigui menor el nombre respecte la longitud de l'array)
          this.checkGeneral();
          this.roverResult = true;
        }
      } else {
        this.roverResult = false; //Si checkInputsAndLimits no retorna true, mostrem per pantalla el missatge FALSE
      }
    },
  },
};
</script>