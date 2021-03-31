<template>
    <div>

        <div class="nav">
            <PrimaryButton value="SIZES" @click="selectTab(1, 'SIZES')" />
            <PrimaryButton value="MOUNTS" @click="selectTab(2, 'MOUNTS')" />
            <PrimaryButton value="FRAMES" @click="selectTab(3, 'FRAMES')" />
        </div>
        <div class="frame-picker-body">

            <div class="frame-props">
                <div class="frame-props-container">
                    <div class="tab" v-show="currentTab==1">
                        <div>
                            <h2>{{ header }}</h2>
                        </div>
                        <div class="frame-props-header"></div>
                        <div class="flex">
                            <div class="half margin-top">
                                WIDTH
                                <div>
                                    <input type="number" v-model="width" class="margin-top align-mid" >
                                    <label class="mm">
                                        mm
                                    </label>
                                </div>
                            </div>
                            <div class="half margin-top">
                                HEIGHT
                                <div>
                                    <input type="number" v-model="height" class="margin-top align-mid">
                                    <label class="mm">
                                        mm
                                    </label>
                                </div>
                            </div>

                        </div>
                        <div class="margin-top30">
                            <button class="btn btn1" @click="adjustCanvas">Apply</button>
                        </div>
                        
                    </div>

                    <div class="tab" v-show="currentTab==2">
                        <div>
                            <h2>{{ header }}</h2>
                        </div>
                        <div class="frame-props-header"></div>
                        <div class="flex">
                            <div class="half margin-top">
                                <div>
                                    <input type="radio" id="single" value="Single Mount" v-model="picked">
                                    <label for="single" class="mount">
                                        Single Mount
                                    </label>
                                </div>
                            </div>
                            <div class="half margin-top">
                                <div>
                                    <input type="radio" id="double" value="Double Mount" v-model="picked">
                                    <label for="double" class="mount">
                                        Double Mount
                                    </label>
                                </div>
                            </div>
                            <div class="half margin-top">
                                <div>
                                    <input type="radio" id="none" value="No Mount" v-model="picked">
                                    <label for="none" class="mount">
                                        No Mount
                                    </label>
                                </div>
                            </div>


                        </div>
                        <div class="margin-top30 color-picker flex" v-if="picked != 'No Mount'">
                            <h3>Pick a Color:</h3> 
                            <ul>
                                <li class="color-item" id="red" @click="changeColor('red')" ></li>
                                <li class="color-item" id="green" @click="changeColor('green')" ></li>
                                <li class="color-item" id="amber" @click="changeColor('#ffca28')" ></li>
                                <li class="color-item" id="blue" @click="changeColor('#42a5f5')" ></li>
                                <li class="color-item" id="gray" @click="changeColor('#bdbdbd')" ></li>
                            </ul>
                        </div>
                        <div class="margin-top30">
                            <button class="btn btn1" @click="pickMount">Apply {{picked}} </button>
                        </div>
                        
                    </div>

                    <div class="tab" v-show="currentTab==3">

                        <div>
                            <h2>{{ header }}</h2>
                        </div>
                        <div class="frame-props-header"></div>

                        
                    </div>

                </div>
            </div>

            <div class="frame-visual">

                <div id="frame" class="frame" :class="{'single-mount': picked=='Single Mount'}">
                    <div class="centered">
                        <span>
                            <b>{{widthRegistered}} x {{heightRegistered}}mm</b>
                        </span>
                    </div>
                </div>
                
            </div>

        </div>

    </div>
</template>

<script>

    import PrimaryButton from './PrimaryButton'

    export default {
        components: {
            PrimaryButton,
        },
        data: function() {
            return {
                header: "SIZES",
                width:"450",
                height:"450",
                widthRegistered:"450",
                heightRegistered:"450",
                maxDimension:"450",
                currentTab: 1,
                picked:"No Mount",
            };
        },
        methods: {
            adjustCanvas: function() {
                var width = parseInt(this.width);
                var height = parseInt(this.height);
                var ratio = 0;

                if (width == height) {
                    document.getElementById('frame').style.width = this.maxDimension + "px";
                    document.getElementById('frame').style.height = this.maxDimension + "px";
                }
                else if (width > height) {
                    ratio = Math.round((height*1.0 / width) * this.maxDimension);
                    console.log(ratio);
                    document.getElementById('frame').style.width = this.maxDimension + "px";
                    document.getElementById('frame').style.height = ratio + "px";
                }
                else {
                    ratio = Math.round((width*1.0 / height) * this.maxDimension);
                    console.log(ratio);
                    document.getElementById('frame').style.height = this.maxDimension + "px";
                    document.getElementById('frame').style.width = ratio + "px";
                }
                this.widthRegistered = this.width;
                this.heightRegistered = this.height;

            },
            selectTab(selectedTab, header) {
                this.currentTab = selectedTab; 
                this.header = header;
            },
            changeColor(color) {
                document.getElementById('frame').style.borderColor = color;
            }
        }
    }
</script>

<style scoped>

.single-mount {
    border-width: 20px;
    border-color: black;
    border-style: solid;
}
span {
    margin: 0;
    padding: 0;
    position: relative;
    text-align: center;
    top: 50%;
    transform: translateY(-50%);
    font-family:'Brush Script MT', cursive;
    font-size: 10px;
}
.nav {
    background: #444;
    text-align: center;
    padding: 4px;
}
.centered {
    display: block;
    margin-left: auto;
    margin-right: auto;
    height: 50%;
}
.frame-picker-body {
    min-height: 88vh;
    display: flex;
}
.flex {
    display: flex;
}
.half {
    width: 50%;
}
.align-mid {
    text-align: center;
}
.margin-top {
    margin-top: 10px;
}
.margin-top30 {
    margin-top: 30px;
}
.frame-props {
    background: rgb(233, 224, 225);
    width: 50vw;
}
.mm{
    background: rgb(124, 113, 113);
    padding-right: 3px;
    padding-bottom: 3px;
    color: white;
}
.mount{
    padding-right: 3px;
    padding-bottom: 3px;
    color: black;
}

.frame-visual {
    background: rgb(193, 231, 255);
    width: 50vw;
}

.frame-props-container {
  width: 80%;
  margin: 30px auto;
  overflow: auto;
  border: 3px solid#444;
  padding: 10px;
  padding-bottom: 60px;
  border-radius: 20px;
}
.frame-props-header {
    background: #444;
    border: 1px solid#444;
    width:100%;
    height:30%;
}
h2 {
    letter-spacing: 5px;
}
input {
    border:2px solid #aaa;
    border-radius: 4px;
    outline:none;
    box-sizing: border-box;
    padding: 4px;
    margin-left: 20px;
}
input:focus {
    border-color: #444;
    box-shadow: 0 0 8px 0 #444;
}
.btn {
    border: 1px solid #3498db;
    background:#444;
    padding: 10px 20px;
    font-size: 20px;
    cursor:pointer;
    transition: 0.8s;
    margin: 10px;
    border-radius: 10px;
}
.btn1 {
    color: #e2e7eb;
}
.btn1:hover {
    color: #fff;
    background:#666;
}
.btn::before{
    content:"";
    left: 0;
    width: 100%;
    height: 0%;
    background: #3498db;
    z-index: -1;
    transition:0.8s;
}
.btn1::before {
    top: 0;
    border-radius: 10px;
}
.btn1:hover::before {
    height: 180%;
}
.frame {
    background: violet;
    width: 450px;
    height: 450px;
    margin: auto;
    margin-top: 60px; 
    box-shadow: 5px 10px 5px rgb(126, 126, 126);
    background-image: url("texture.jpeg");
    display: flex;
    align-items: center;
    justify-content: center;
}
.art-size {
    margin: auto;
    display: flex;
    justify-content: center;
}
ul {
    list-style: none;
    padding: 24px;
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    grid-gap: 20px;
}
ul li {
    width:24px;
    height: 24px;
    background-color: red;
    border: 2px solid black;
    border-radius: 30%;
    cursor: pointer;
}
ul li:hover {
    transform: scale(1.1);
}

.color-picker {
    justify-content: center;
    align-items: center;
}

#red {
    background-color: red;
}
#green {
    background-color: green;
}
#amber {
    background-color: #ffca28;
}
#blue {
    background-color: #42a5f5;
}
#gray {
    background-color: #bdbdbd;
}

</style>