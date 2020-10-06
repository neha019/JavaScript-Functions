# WebRTC 

WebRTC is a protocol based Real Time Communication natively between browsers. End-users do not have to download a special software application or use the client or browser plug-in to communicate directly with each other.
Simply put : WebRTC enables for voice and video communication to work inside web pages.

# WebRTC JavaScript API's

WebRTC are implemented through a set of JS API's that actually produce and transmit the multimedia data being used for real time communication. The three main components in WebRTC are as stated below :
- Navigator.mediaDevices.getUserMedia aka MediaStream (captures audio and video)
- RTCPeerConnection (creates and negotiates peer to peer connection)
- RTCDataChannel (represents a bidirectional data channel between peers)

> ## MediaDevices.getUserMedia()

It prompts the user for permission to use a media input which produces a MediaStream with tracks containing the requested types of media. The stream can include for e.g. - a video track, an audio track, and posiibly other track types.

It returns a Promise that resolves to a MediaStream object. If user denies permission, then promise is rejected with PermissionDeniedError or NotFoundError respectively.

``` javascript
navigator.mediaDevices.getUserMedia(constraints).
then((stream) => {
    // use the stream
}).catch((error) => {
    // handle the error
});
```
> ### Syntax :
``` javascript
var promise = navigator.mediaDevices.getUserMedia(constraints, successCallback, errorCallback);
```
constraints is an object specifying the types of media to request along with any requirements for each type
``` javascript
var constraints = {
    audio : true,
    video : true
};
```
It returns a Promise whose fulfillment handler receives a MediaStream object when the requested media has successfully been obtained.

Each localmedia has a label, audioTracks and videoTracks properties each of which is a MediaStreamTrackList.

### Capturing a LocalMedia Stream 
``` javascript
navigator.mediaDevices.getUserMedia(constraints). 
then((stream) => {
    var local = document.getElementById('local-video');
    local.src = window.URL.createObjectURL(stream);
    // or we can use srcObject property, URL.createObjectURL() is now deprecated
    local.srcObject = stream;
}).catch((error) => {
    console.log('error in accessing local media stream : ', error);
});
```

> ## RTCPeerConnection 

The RTCPeerConnection represents the connection between two independent browsers together so that they can share a real-time media. It allows us to connect to a remote peer, oversees the connection and close it once the communication is completed. 

### Steps to initiate RTCPeerConnection :

- The RTCPeerConnection API is built for JavaScript. In order for two peer connections to work, RTCPeerConnection(pc) must acquire the local media stream.
- After obtaining the media stream through getUserMedia API, next step is to transmit the captured media to other browsers.
- An offer is created (from the local peer connection) and extended to the other browser (to remote peer connection) with the help of Session Description Protocol aka SDP.
- After the description(offer) is generated it is sent to a remote peer connection.
- When the offer is received by the remote peer connection on other side, they generate an answer which is then acknowledged back to the initiator(local peer).
- When both the parties are done with offering and answering session, they can see local and remote peers video for communicating further.

> ## RTCPeerConnection Methods (Commonly Used) : 

- **createOffer()**  
It initiates the creation of SDP offer for establishing a new WebRTC connection to connect to a remote peer. It includes info about MediaStreamTracks, codec, browser supported, any ICE candidate gathered. The return value is a promise, when offer is created it is resolved by RTCSessionDescription object containing the newly created offer.
```javascript
var pc = new RTCPeerConnection();
//creating an offer
pc.createOffer().then((offer) => {
    return pc.setLocalDescription(offer);
}).catch((error) => {
    console.log('error : ', error);
});
``` 
Once offer is created RTCPeerConnection is configured to pass the offer into setLocalDescription(). When that's done, offer is sent to remote peer connection.

- **setLocalDescription()**  
It changes the local description associated with the connection. It specifies the properties of the local end of the connection including media format. The description submitted by setLocalDescription() doesnt take effect immidiately.
```javascript
pc.createOffer().then((offer) => {
    return pc.setLocalDescription(offer);
});
``` 
When the offer is created successfully, setLocalDescription method is called. Once the Promise is fulfilled, the newly created offer can then be sent to other peer connection.

- **createAnswer()**  
It creates an SDP answer to an offer received from the remote peer during the offer/answer negotiation. 
```javascript 
var pc = new RTCPeerConnection();
pc.createAnswer().then((answer) => {
    return pc.setLocalDescription(answer);
}).catch((err) => {
    console.log('error : ', err);
});
``` 
RTCPeerConnection creates and return a new answer. The returned answer is set as description for local peer connection by calling setLocalDescription(). Once the answer is generated it is sent to the initiator of the offer.

- **setRemoteDescription()**  
It changes the remote description associated with the connection and returns a Promise which is fulfilled once the description has been changed asynchronously. It is called whenever offer or answer is received from another peer. 
```javascript 
pc.setRemoteDescription(description).then(() => {
    return;
});
``` 
Here the argument passed _description_ is the offer received by the local peer connection. Once the remote description is set for both the peers (offer and answer), then webRTC conncetion is established successfully for caller and callee.

# WebRTC Protocols/Media Connections :

> ## NAT 
NAT stands for Network Address Translation. It is usually placed between a private network(LAN) and the public network(Internet). These translates internal private IP addresses to external public IP addresses. NAT is basically used to prevent any discrepancies of our bisiness and personal data, it acts as a security wall between the private and public networks to prevent leak of any confidential info in the outside world. Each TCP/IP and UDP/IP packet contains a stack of information that it carries with it as it travels around the internet. 

NAT allows a single device, such as router to act an intermediate between the Internet and a local network which means a single unique IP address is required to represent an entire group of computers to anything outside their network.

> ## STUN 
STUN stands for Session Traversal Utilities for NAT. It tells clients what their public NAT'd IP address and port is. In this protocol, the client sends request to STUN server on the Internet who will reply with the client's public address whether it is accessible behind the router's NAT or not. STUN server is usually used during the session connection setup, once it is done media will flow directly between clients. If it cannot establish connection, ICE can turn to TURN.

> ## TURN 
TURN stands for Traversal Using Relay NAT. It is used to relay audio, video and data streaming between peers. TURN servers have the info about the public addresses assigned to each client in the network, through which they can contact peers even if they are behind the firewall or proxies. Usually TURN and STUN servers are deployed together. It bypasses "Symmetric NAT" restriction by openeing a connection to TURN server and tramsfers all streaming data between two peers.

> ## ICE 
ICE stands for Interactive Connectivity Establishment. It is a freamework which allows the two browsers to connect to each other aka peer-to-peer connection. ICE uses STUN/TURN servers to bypass the firewall prevents openeing connection, assigns a unique IP address and then relays data between two peers successfully. 