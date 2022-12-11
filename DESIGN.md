# recording-score

Design for Project

Main three javascript functions are used to represent the web design and function.

================================================================================

Part 1: queue of threads

Recording score needs a playlist queue of threads.

Recording would be played by hovering the cursor on “lyric”:

    const toggleVideo = (ev) => {
        const EL = ev.currentTarget;
        const EL_video = EL.querySelector("video");
        const isPlay = ev.type === "mouseenter";
        EL_video[isPlay ? "play" : "pause"]();
    };

Actucally “lyric” include the video file, therefore hovering the cursor on “lyric” means hovering the cursor on "video"

    const ELS_aVid = document.querySelectorAll(".hoverVid");

    ELS_aVid.forEach(EL => {
        ["mouseenter", "mouseleave"]
        .forEach(evt => EL.addEventListener(evt, toggleVideo))
    });

================================================================================

Part 2: Thread Class

The metadata of the recording is hidden under the lyrics.

And this is implemented by openAndClose_drawer function and conditional syntax.

    function openAndClose_drawer(elm) {
        var selected_drawer = elm.nextSibling.nextSibling;

        if (elm.classList.contains("opened")) {
            elm.classList.remove("opened")

            if (selected_drawer.classList.contains("closed")) {
            }
            else {
                selected_drawer.classList.add("closed")
            }
        }
        else {
            elm.classList.add("opened")
            selected_drawer.classList.remove("closed")
        }

        var hist_str = "#/temp"
        window.history.pushState(hist_str, 'Title', hist_str);

    }

================================================================================

Part 3: Randomize Class

Randomize function is important to this design, because it make playlist's passive sequence massive, but also active.
User use the Two or more voices button to make sequence random.
By using randomize fuction, user could read the their own text, and it is a minimal interation gesture.

    function randomizeContent(classname){
        var contents=randomizeContent.collectElementbyClass(classname)

        contents.text.sort(function() {return 0.5 - Math.random();})
    
        var tbodyref=contents.ref[0].tagName=="TR"? contents.ref[0].parentNode : new Object()

        for (var i=0; i<contents.ref.length; i++){
            if (tbodyref.moveRow) {
                //if IE
             tbodyref.moveRow(0, Math.round(Math.random()*(tbodyref.rows.length-1)))
            }
            else {
             contents.ref[i].innerHTML=contents.text[i]
             contents.ref[i].style.visibility="visible"
            }
        }
    }

randomizeContent.collectElementbyClass=function(classname){
    //return two arrays containing elements with specified classname, plus their innerHTML content
    var classnameRE=new RegExp("(^|\\s+)"+classname+"($|\\s+)", "i")

    //regular expression to screen for classname within element
    var contentobj=new Object()
    
    contentobj.ref=new Array() //array containing references to the participating contents
    contentobj.text=new Array() //array containing participating contents' contents (innerHTML property)
    
    var alltags=document.all? document.all : document.getElementsByTagName("*")

    for (var i=0; i<alltags.length; i++){
        if (typeof alltags[i].className=="string" && alltags[i].className.search(classnameRE)!=-1){
            contentobj.ref[contentobj.ref.length]=alltags[i]
            contentobj.text[contentobj.text.length]=alltags[i].innerHTML
        }
    }

================================================================================