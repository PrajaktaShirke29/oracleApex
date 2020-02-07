This project is to convert text to speech using [Oracle Apex](https://apex.oracle.com/en/).

Below you will find some information on how to perform tasks.<br>

## Table of Contents

- [Demo Application](#demo-application)
- [Create Workspace in Apex Oracle before login](#create-workspace-in-apex-oracle-before-login)
- [SignIn on Apex Oracle](#sign-in-on-apex-oracle)
- [Create Application](#create-application)
- [Create UI for the project convert text to speech](#create-ui-for-the-project-convert-text-to-speech)
- [Apply javascript to convert text into speech](#apply-javascript-to-convert-text-to-speech)
- [Conclusion](#conclusion)


## Demo Application
Demo of [Text To Speech](#https://apex.oracle.com/pls/apex/f?p=49473:LOGIN_DESKTOP:15816013180148) will give you the basic idea of the application.

[Demo Applicalication](https://apex.oracle.com/pls/apex/f?p=49473:LOGIN_DESKTOP:15816013180148)


## Create Workspace in Apex Oracle before login

[Create Workspace](https://apex.oracle.com/en/learn/getting-started/) :
*  Click on `Request a Free Workspace` on [Oracle Apex](https://apex.oracle.com/en/).
*   In which you need to provide some basic information: Name, email, Are you new to this apex oracle? and why you need this workspace for?
*   Mail is send on the email provided for confirmation of the workspace and password setting.


## SignIn on Apex Oracle

*  In this you need to proved the workspace and email which in provided in mail  and password which is been set by you.

## Create Application

Know You need to create the application:
* Go to App builder and then create with + icon.
* New Application : This will the application with the login, home and administration implicitly.
* Create an Application page: 
    * Add you project name
    * Check all the features
    * Create application

This will create your application.


##  Create UI for the project convert text to speech

For this you need to navigate to home page i.e Page 1, then navigate to breadcrumb bar.

Edit region: Source will be
`<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css">

<div class="container">
    <div class="row">
        <nav>
            <div class="nav-wrapper">
                <div class = "col s12">
                    <a href="#" class="brand-logo"> Text To Speech example</a>
                </div>    
            </div>
        </nav>
    </div>
    <form class = "col s8 offset-s2">
        <div class="row">
            <label>Choose voice</label>
            <select id="voices"></select>
        </div>
        <div class="row">
        <div class="col s6">
            <label>Rate</label>
            <p class="range-field">
                <input type="range" id="rate" min="1" max="100" value="10" />
            </p>
        </div>
        <div class="col s6">
            <label> Pitch</label>
            <p class="range-field">
                <input type="range" id="pitch" min="0" max="2" value="1" />
            </p>
        </div>
        </div>
        <div class = "col s12">
            <p>
                N.B Rate and Pitch only work with native voice.
            </p>
        </div>
        <div class="row">
            <div class="input-field col s12">
                <textarea id="message" class="materialize-textarea"></textarea>
                <label> Write message </label>
            </div>
        </div>
        <a href="#" id="speak" class="waves-effect waves-light btn">Speak</a>
    </form>
</div>
<div id="modal1" class="modal">
    <h4>Speech Synthesis not supported.</h4>
    <p>Your browser does not support speech sunthesis.</p>
    <p>We recommend you use Google chrome.</p>
    <div class="action-bar">
        <a href="#" class="waves-effect waves-green btn-flat modal-action modal-close"> Close</a>
    </div>
</div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.3/jquery.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/js/materialize.min.js"></script>`

Then in apperance: Template must be select.
Then run the application you will be able to see the UI. You can modify the you as per your request.

## Apply javascript to convert text into speech

For this you need to navigate to home page i.e Page 1, select home in the layout.

Edit the page: javascript -> Function and Global Variable Declaration as
$(function(){
    if('speechSynthesis' in window){
        speechSynthesis.onvoiceschanged = function() {
            var $voicelist = $('#voices');
            if($voicelist.find('option').length == 0){
                speechSynthesis.getVoices().forEach(function(voice, index){
                    var $option = $('<option>')
                    .val(index)
                    .html(voice.name + (voice.default ? ' (default)': ''));
                    
                    $voicelist.append($option);
                });
                $voicelist.material_select();
            }
        }
        $('#speak').click(function(){
            var text = $('#message').val();
            var msg = new SpeechSynthesisUtterance();
            var voices = window.speechSynthesis.getVoices();
            msg.voice= voices[$('#voices').val];
            msg.rate = $('#rate').val() / 10;
            msg.pitch = $('#pitch').val();
            msg.text = text;
            msg.onend = function(e){
                console.log('Finished in '+event.elapsedTime+ ' seconds.');
            };
            speechSynthesis.speak(msg);
        })
        $('#modal1').openModal();
    }
})

This will make your application running on apex oracle.

## Conclusion

This application will give you the basic information of how to create the oracle application with the javascript and UI in dynamic way.

This application has limit to the converter where crome can convert only 44 words, [etc](https://developer.mozilla.org/en-US/docs/Web/API/SpeechSynthesis)