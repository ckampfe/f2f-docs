OBJECTIVE: Build an app that allows for drag-and-drop p2p file transfer between
2 users (1-to-1 user basis).

  The users should be anonymous.

  The initiating user drags a file to the app window and gets presented with a
link to provide to the receiving user.
  The initiating user must keep the browser tab open until the file is fully
transferred to the receiver.

  Receiving user must click a link to initiate download of desired file.
  Once receiver has downloaded the file, the connection is terminated and the
link is dead.

  Initiator is notified once download is complete, so they can close the tab.

  PHASE 1 - SENDER UPLOAD PHASE (SENDER END ONLY)
  STEP 1: User visits www.quickbit.com
    MAY USE: HTML5 & CSS (virtually mandatory), Some page server (may or may
      not be Rails) (required).

  STEP 2: Sending user drags a file to upload window. File (or file location) is
saved by the app on the user's machine.
    MAY USE: Javascript (probably required)
    OPEN QUESTSIONS:
[Chirag]    - How do we go about reading that file (location only?)
       from  disk with JS given browser's security about disk read operations?
    - Will we need to save the file's location in the DOM? Or a JS variable?

  STEP 3: A link is generated and provided to the user. This link can be given
    to the person who wants to download the file.
    MAY USE: ???
    OPEN QUESTIONS:
      - How are those links generated? And by what (Rails, JS, some service we
        are using?)?
      - How do we guarantee that each link is unique?
      - Should a link contain an initiating_user_id of some sort? If not, how
        will the receiver know who to connect to?

  PHASE 2 - RECIEVER DOWNLOAD PHASE (SENDER AND RECIEVER):
  STEP 4: Receiving user clicks a quickbit file download link and is taken to
    that page.

  STEP 5: Upon completion of page load, the receiving user establishes a
connection with the sending user provided that the sending user is still
connected.
    MAY USE: Some sort of handshaking service (Peer.js, WebRTC, WebSockets,
other possibilities)
    OPEN QUESTIONS:
      - Do we need to explicitly handle what happens if no connection can be
        established or just have a view that pops up that informs the user that
they failed to establish a connection with the sending user.

  STEP 6: File transfer from sender to receiver begins.
    MAY USE: ???
    OPEN QUESTIONS:
      - What protocol is used for this file transfer (HTTP? TCP? FTP? Something
        else)?
      - What data format(s) are used when the file is loaded and prepared for
        transfer in the sender's browser?
      - Do we need to load the whole file into memory before the transfer begins
        or can it be done in chunks as transfer is in progress.
      - Does the whole file have to be transfered and received by the receiver
        before it is saved to the receiver's disk?

  STEP 7: File transfer ends, the receiver is informed of this, and the file is
now fully saved on the receiver's local machine.

  STEP 8: Connection is closed.
    OPEN QUESTION:
      - Is the link invalidated? If so, how?

  STEP 9: Sender is informed that the receiver download is complete and that it
is safe to close the browser.


  EDGE CASE: What happens if a sender closes their browser in the middle of a
transfer? How do we know if this occurs? Some sort of timeout?

  OTHER QUESTIONS:
    - Is WebRTC cross browser compliant across Firefox and Chrome?
    - What kind of iOS browser support is there for WebRTC, if any?
