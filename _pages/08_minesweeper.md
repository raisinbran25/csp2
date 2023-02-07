---
title: minesweeper
layout: default
description: 
---
<!-- Style (CSS) implementation of the map. -->
<style>
/* class to create the map's container; uses CSS grid dsiplay to partition off buttons */
.map-container { 
    width: 500px; /* this width and height is specified for mobile devices by default */
    height: 500px;
    right: 50px;

    display: grid;
    grid-template-columns: repeat(8, 1fr); /* fr is a special unit; learn more here: https://css-tricks.com/introduction-fr-css-unit/  */
    grid-template-rows: repeat(8, 1fr);
    gap: 1px 1px;
}

/* 
    CSS allows programmers to use media queries to change the size of classes based on the size of the device.
    This allows us to make it so that our website looks good on both mobile and desktop. If the width of the
    device is big enough, then the map will take up more of the screen.
*/
@media (min-width: 100px) { 
    .map-container {
        width: 50px;
        height: 50px;
        left: 20px
    }
}

/* styling for the map buttons themselves */
.map-blankbutton {
    width: 40px;
    height: 40px;
    border-radius: 0px;
    background-color: #90EE90;
    border: 0px solid black;
    font-size: 1.5fem;

    display: flex;
    justify-content: center;
    align-items: center;

    /* grid display allows programmer to specify how much of the grid an element should take up; these buttons will take up 1 row and 1 column */
    grid-column: span 1;
    grid-row: span 1;

    /* allows for smooth transition of properties and the "animation" effect to appear on hover */
    transition: all 0s; 
}

.map-zerobutton {
    width: 40px;
    height: 40px;
    border-radius: 0px;
    background-color: #D2B48C;
    border: 0px solid black;
    font-size: 1.5fem;

    display: flex;
    justify-content: center;
    align-items: center;

    /* grid display allows programmer to specify how much of the grid an element should take up; these buttons will take up 1 row and 1 column */
    grid-column: span 1;
    grid-row: span 1;

    /* allows for smooth transition of properties and the "animation" effect to appear on hover */
    transition: all 0s; 
}

.map-minebutton {
    width: 40px;
    height: 40px;
    border-radius: 0px;
    background-color: #AA4A44;
    border: 0px solid black;
    font-size: 1.5fem;

    display: flex;
    justify-content: center;
    align-items: center;

    /* grid display allows programmer to specify how much of the grid an element should take up; these buttons will take up 1 row and 1 column */
    grid-column: span 1;
    grid-row: span 1;

    /* allows for smooth transition of properties and the "animation" effect to appear on hover */
    transition: all 0s; 
}

.map-numberbutton {
    width: 40px;
    height: 40px;
    border-radius: 0px;
    background-color: #D2B48C;
    border: 0px solid black;
    font-size: 1.5fem;

    display: flex;
    justify-content: center;
    align-items: center;

    /* grid display allows programmer to specify how much of the grid an element should take up; these buttons will take up 1 row and 1 column */
    grid-column: span 1;
    grid-row: span 1;

    /* allows for smooth transition of properties and the "animation" effect to appear on hover */
    transition: all 0s; 
}

.map-longbutton {
    width: 328px;
    height: 80px;
    border-radius: 0px;
    background-color: #000000;
    border: 0px solid black;
    font-size: 1.5fem;

    display: flex;
    justify-content: center;
    align-items: center;

    /* grid display allows programmer to specify how much of the grid an element should take up; these buttons will take up 1 row and 1 column */
    grid-column: span 8;
    grid-row: span 2;

    /* allows for smooth transition of properties and the "animation" effect to appear on hover */
    transition: all 0s; 
}

/* darkens the background color on hover to create a selecting effect */
.map-blankbutton:hover {
    background-color: #373737;
}
.map-longbutton:hover {
    background-color: #373737;
}
</style>


<!-- HTML implementation of the map. 
    CSS sets 4 buttons (map-blankbutton) to a row
    All buttons have onclick JavaScript action
    All actions result in map-output.innerHTML change
-->
number of mines:<input type="text" id="button" value="">
    <button type="button" onclick="enter()">Enter</button>
<div class="map-container">
    <div class="map-longbutton" id="reset" onclick="initialize()">click here to play!</div>
    <!--row 1-->
    <div class="map-blankbutton" id="b18"></div>
    <div class="map-blankbutton" id="b28"></div>
    <div class="map-blankbutton" id="b38"></div>
    <div class="map-blankbutton" id="b48"></div>
    <div class="map-blankbutton" id="b58"></div>
    <div class="map-blankbutton" id="b68"></div>
    <div class="map-blankbutton" id="b78"></div>
    <div class="map-blankbutton" id="b88"></div>
    <!--row 2-->
    <div class="map-blankbutton" id="b17"></div>
    <div class="map-blankbutton" id="b27"></div>
    <div class="map-blankbutton" id="b37"></div>
    <div class="map-blankbutton" id="b47"></div>
    <div class="map-blankbutton" id="b57"></div>
    <div class="map-blankbutton" id="b67"></div>
    <div class="map-blankbutton" id="b77"></div>
    <div class="map-blankbutton" id="b87"></div>
    <!--row 3-->
    <div class="map-blankbutton" id="b16"></div>
    <div class="map-blankbutton" id="b26"></div>
    <div class="map-blankbutton" id="b36"></div>
    <div class="map-blankbutton" id="b46"></div>
    <div class="map-blankbutton" id="b56"></div>
    <div class="map-blankbutton" id="b66"></div>
    <div class="map-blankbutton" id="b76"></div>
    <div class="map-blankbutton" id="b86"></div>
    <!--row 4-->
    <div class="map-blankbutton" id="b15"></div>
    <div class="map-blankbutton" id="b25"></div>
    <div class="map-blankbutton" id="b35"></div>
    <div class="map-blankbutton" id="b45"></div>
    <div class="map-blankbutton" id="b55"></div>
    <div class="map-blankbutton" id="b65"></div>
    <div class="map-blankbutton" id="b75"></div>
    <div class="map-blankbutton" id="b85"></div>
    <!--row 5-->
    <div class="map-blankbutton" id="b14"></div>
    <div class="map-blankbutton" id="b24"></div>
    <div class="map-blankbutton" id="b34"></div>
    <div class="map-blankbutton" id="b44"></div>
    <div class="map-blankbutton" id="b54"></div>
    <div class="map-blankbutton" id="b64"></div>
    <div class="map-blankbutton" id="b74"></div>
    <div class="map-blankbutton" id="b84"></div>
    <!--row 6-->
    <div class="map-blankbutton" id="b13"></div>
    <div class="map-blankbutton" id="b23"></div>
    <div class="map-blankbutton" id="b33"></div>
    <div class="map-blankbutton" id="b43"></div>
    <div class="map-blankbutton" id="b53"></div>
    <div class="map-blankbutton" id="b63"></div>
    <div class="map-blankbutton" id="b73"></div>
    <div class="map-blankbutton" id="b83"></div>
    <!--row 7-->
    <div class="map-blankbutton" id="b12"></div>
    <div class="map-blankbutton" id="b22"></div>
    <div class="map-blankbutton" id="b32"></div>
    <div class="map-blankbutton" id="b42"></div>
    <div class="map-blankbutton" id="b52"></div>
    <div class="map-blankbutton" id="b62"></div>
    <div class="map-blankbutton" id="b72"></div>
    <div class="map-blankbutton" id="b82"></div>
    <!--row 8-->
    <div class="map-blankbutton" id="b11"></div>
    <div class="map-blankbutton" id="b21"></div>
    <div class="map-blankbutton" id="b31"></div>
    <div class="map-blankbutton" id="b41"></div>
    <div class="map-blankbutton" id="b51"></div>
    <div class="map-blankbutton" id="b61"></div>
    <div class="map-blankbutton" id="b71"></div>
    <div class="map-blankbutton" id="b81"></div>
</div>


<!-- JavaScript (JS) implementation of the map(backend) -->
<script>
//user input
numines = null
function enter() {
    input = document.getElementById("button").value
    if (input > 0) {
        numines = input
    }
}
// timer code
starttime = null
finaltime = null
min = 00
sec = 00
hsec = 00
function updatetime() {
    time = Math.floor((finaltime - starttime) / 10)
    min = Math.floor(time / 6000)
    if (min < 10) {
        min = "0" + String(min)
    }
    else {
        min = String(min)
    }
    time = time % 6000
    sec = Math.floor(time / 100)
    if (sec < 10) {
        sec = "0" + String(sec)
    }
    else {
        sec = String(sec)
    }
    time = time % 100
    hsec = time
    if (hsec < 10) {
        hsec = "0" + String(hsec)
    }
    else {
        hsec = String(hsec)
    }
    
    document.getElementById("reset").innerHTML = "congratulations! you won with a time of " + min + ":" + sec + "." + hsec + "! click here to reset." 
}

// minesweeper code
winstatus = null
mines = { // object storing ids and number of surrounding mines
    cord: {

    }
}
nums = [] // all possible ids
mids = [] // ids of mines

function addcords() {
    for (let i = 11; i < 90; i++) {
        if (String(i)[0] != "9" && String(i)[0] != "0") {
            if (String(i)[1] != "9" && String(i)[1] != "0") {
                mines.cord[i] = {"ms" : 0}
                nums.push(i)
            }
        }
    }
}
function placemines() { // adds ms value "9" in object
    while (mids.length < numines) { // place 10 mines
        r = Math.floor(Math.random() * 64)
        if (mines.cord[nums[r]]["ms"] == 0) { //avoid repeat mines
            mines.cord[nums[r]]["ms"] = 9
            mids.push(nums[r])
        }
    }
}
function calcmines() { // updates all other ms values in object
    dvals = [-11, -10, -9, -1, 1, 9, 10, 11]
    for (let i = 0; i < mids.length; i++) { //each mine
        for (let j = 0; j < dvals.length; j++) { //each difference value
            try { //in case coordinate does not exist
                mines.cord[mids[i] + dvals[j]]["ms"] += 1
                if (mines.cord[mids[i] + dvals[j]]["ms"] > 9){
                    mines.cord[mids[i] + dvals[j]]["ms"] -= 1
                }
            }
            catch(err) {
            }
        }
    }
}
function play() { // button functions and class
    if (numines == null) {
        return
    }
    for (let i = 0; i < nums.length; i++) {
        cord = String(nums[i])
        bname = document.getElementById("b" + cord)
        bname.className = "map-blankbutton"
        if (mines.cord[nums[i]]["ms"] == 0) {
            bname.className = "map-zerobutton"
        }
        else if (mines.cord[nums[i]]["ms"] == 9) {
            bname.addEventListener("click", mine.bind(null, cord))
        }
        else {
            bname.addEventListener("click", number.bind(null, cord)) //null is for specific button, cord is parameter in "number" function
        }
    }
    document.getElementById("reset").innerHTML = "" 
    document.getElementById("reset").onclick = null
    inprogress = true
    starttime = Date.now()
}
function number(cord) { // reveal number
    if (winstatus != null) {
        return
    }
    bname = document.getElementById("b" + String(cord))
    bname.className = "map-numberbutton"
    bname.innerHTML = String(mines.cord[String(cord)]["ms"])
    checkwin()
}
function mine() { // game over
    if (winstatus == true) {
        return
    }
    inprogress = false
    winstatus = false
    for (let i = 0; i < nums.length; i++) {
        cord = String(nums[i])
        bname = document.getElementById("b" + cord)
        if (mines.cord[nums[i]]["ms"] == 0) {
            bname.className = "map-zerobutton"
        }
        else if (mines.cord[nums[i]]["ms"] == 9) {
            bname.className = "map-minebutton"
        }
        else {
            bname.className = "map-numberbutton"
            bname.innerHTML = String(mines.cord[String(cord)]["ms"])
        }
    }
    bname = document.getElementById("reset")
    bname.innerHTML = "you lost! click here to reset."
    bname.addEventListener("click", function () {
        window.location.reload()
    })
}
function checkwin() {
    if (winstatus == false) {
        return
    }
    for (let i = 0; i < nums.length; i++) {
        cord = String(nums[i])
        bname = document.getElementById("b" + cord)
        if (mines.cord[nums[i]]["ms"] > 0 && mines.cord[nums[i]]["ms"] < 9) {
            if (bname.className == "map-blankbutton") {
                return
            }
        }
    }
    winstatus = true
    win()
}
function win() {
    for (let i = 0; i < nums.length; i++) {
        cord = String(nums[i])
        bname = document.getElementById("b" + cord)
        if (mines.cord[nums[i]]["ms"] == 9) {
            bname.className = "map-minebutton"
        }
        else {
            bname.className = "map-blankbutton"
            bname.addEventListener("click", null)
            bname.innerHTML = "🌸"
        }
    }
    bname = document.getElementById("reset")
    bname.addEventListener("click", function () {
        window.location.reload()
    })
    finaltime = Date.now()
    updatetime()
}
function initialize() {
    addcords()
    placemines()
    calcmines()
    play()
     
}
</script>