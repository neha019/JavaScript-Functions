# Web Components 

Web Components is a collection of web platform API's allowing us to create re-usable custom elements with their functionality encapsulated from the rest of the code and use them in our apps.

It consists of four main concepts, but right now we are focussing mainly on three concepts which are as follows :

- Custom-Elements
- Shadow DOM
- HTML Templates 

# Advantages of Web Components 

The two salient features of Web Components are :

- Declarative Nature
- Seamless Interoperability

# Why Use TokBox JS SDK with Web Components :

We are trying to make TokBox JS SDK more declarative and simplified in nature so that any novice users/ beginners can easily use our WC+JS SDK library to create any TokBox application. 


# Implementation of Web Components with TokBox JS SDK :

Our plan is to create a sample video chat application with the help of Web Components wherein using TokBox JS SDK. 

First UseCase is **_1-1 chat application_** where publihser streams in the session and the subscriber connects to the stream using its streamid in the session.

![](1-1.png?raw=true) 


Second UseCase is **_1-Many chat application_** where one publisher streams in the session and more than one subscriber connects to publisher using its streamid in the session.

![](1-M.png?raw=true) 


# Creation of Custom Web Components with TokBox JS SDK: 

Create index.html file and add one custom tag ot-session with three properties _apikey_, _sessionId_ and _token_ like this :

```html
<ot-session apikey="" sessionId="" token=""> 
</ot-session> 
``` 
This is an example of custom component in the index.html file :
```html 
<ot-session id="session" apikey="45302552" 
sessionId="1_MX40NTMwMjU1Mn5-MTUzMDc4NzUyNTQ2OH51MG1VNTBidUFEQitZTG5vb0RKdnB3bW5-fg"
token="T1==cGFydG5lcl9pZD00NTMwMjU1MiZzaWc9MWM5MWE1NTlmNDQwOTNiMWE1M2ZlNDdlZWJjNTcyYmI0Y2JjMGY0NzpzZXNzaW9uX2lkPTFfTVg0ME5UTXdNalUxTW41LU1UVXpNRGM0TnpVeU5UUTJPSDUxTUcxVk5UQmlkVUZFUWl0WlRHNXZiMFJLZG5CM2JXNS1mZyZjcmVhdGVfdGltZT0xNTMwNzg3NTI2Jm5vbmNlPTAuMjU2NTgxMTAxNDExNTk3OTYmcm9sZT1wdWJsaXNoZXImZXhwaXJlX3RpbWU9MTUzMDg3MzkyNiZpbml0aWFsX2xheW91dF9jbGFzc19saXN0PQ=="> 

</ot-session>
``` 
A custom element can be created using customElements.define() browser API method and class extending HTMLElement in JavaScript shown below :

```javascript 
class OTSession extends HTMLElement {
    //Define functionality here
} 

customElements.define('ot-session', OTSession); 
``` 

> **Accessing html properties in .js file :**

This can be achieved like :

```javascript 
class OTSession extends HTMLElement {
    get apikey() {
        return this.api
    }

    set apikey(value) {
        this.api = value;
        this.setAttribute('apikey');
    }

    get sessionId() {
        return this.sess;
    }

    set sessionId(value) {
        this.sess = value;
        this.setAttribute('sessionId');
    }

    get token() {
        return this.tok;
    }

    set token(value) {
        this.tok = value;
        this.setAttribute('token');
    }
}
``` 

## Publisher connecting to the Session and Session creation : 

After accessing apikey, sessionId and token, initializeSession() method is called which first initializes session object which takes two parameters and returns session object :

```javascript 
this.sessionD = OT.initSession(this.api, this.sess); 
``` 

Now, the client(publisher) connects in the session by calling connect() method like this :

```javascript 
this.sessionD.connect(this.tok, function (error) {
    if (error) {
        console.log('error in connection');
    } else {
        console.log('connected the session');
    }
}); 
``` 
Here, the publisher connects dynamically in the session by creating shadowroot through _template_ : 

```javascript 
static getTemplate() {
    var template = `
    <publisher-video id="publisher">
    </publisher-video>
        `;
    return template;
} 
//creating template and attaching shadowRoot to it
var temp = document.createElement('template');
temp.innerHTML = OTSession.getTemplate()
var tInstance = temp.cloneNode(true);
var clone = document.importNode(tInstance.content, true);
console.log(temp);
this.myShadow = this.attachShadow({ mode: 'open' }).appendChild(clone);

var pub1 = this.shadowRoot.querySelectorAll('#publisher');
``` 

## Subscribing to Publisher's stream : 

The Session object fires an event _streamCreated_ whenever a new stream is created in the session when a publisher publishes in the session. 

```javascript 
var sessionC = document.getElementById('session');
sessionC.addEventListener('streamCreated', function (event) {
    this.sessionD.subscribe(event.stream, 'subscriber-video', function (error) {
        if (error) {
            console.log('error in subscribing');
        } else {
            console.log('subscriber added');
            alert('new subscriber added');
        }
    });
});
``` 

# Additional Properties to be added in Custom elements : 

> ## **Publish Video Only** 

There is an option in TokBox JS SDK, where if publisher wants to publish only video stream in the session. This is one of the property we are including in our custom tag where its value is toggled on or off - publishVideo.

```javascript 
var pubC = this.shadowRoot.querySelectorAll('#publisher');
 var pubVid=this.publishing.publishVideo(true); 

 publisher.on('streamCreated', function(event){
     pubC[0].setAttribute('publishVideo', pubVid.stream.hasVideo);
 });
 ``` 

 > ## **Publish Audio Only** 

 There is an option in TokBox JS SDK, where if publisher wants to publish only audio stream in the session. This is one of the property we are including in our custom tag where its value is toggled on or off - publishAudio.

```javascript 
var pubC = this.shadowRoot.querySelectorAll('#publisher');
 var pubVid=this.publishing.publishAudio(true); 

 publisher.on('streamCreated', function(event){
     pubC[0].setAttribute('publishAudio', pubVid.stream.hasAudio);
 });
 ``` 

 