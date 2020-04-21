# Test Plan

Below are a set of user interactions that are expected to work consistently across all
Link-enabled apps. In order to provide the best user experience, it's important that apps
behave consistently with respect to these test cases. ## Tempo Changes

### TEMPO-1: Tempo changes should be transmitted between connected apps.

- Open LinkHut, press **Play**, when using QLinkHut click the **Link** button to enable
Link. - Open App and **enable** Link. - Without starting to play, change tempo in App
**&rArr;** LinkHut clicks should speed up or slow down to match the tempo specified in
the App. - Start playing in the App **&rArr;** App and LinkHut should be in sync - Change
tempo in App and in LinkHut **&rArr;** App and LinkHut should remain in sync

### TEMPO-2: Opening an app with Link enabled should not change the tempo of an existing Link session.

- Open App and **enable** Link. - Set App tempo to 100bpm. - Terminate App. - Open
LinkHut, press **Play** and **enable** Link. - Set LinkHut tempo to 130bpm. - Open App
and **enable** Link. **&rArr;** Link should be connected (“1 Link”) and the App and
LinkHut’s tempo should both be 130bpm.

### TEMPO-3: When connected, loading a new document should not change the Link session tempo.

- Open LinkHut, press **Play**, when using QLinkHut click the **Link** button to enable
Link. - Set LinkHut tempo to 130bpm. - Open App and **enable** Link **&rArr;** LinkHut’s
tempo should not change. - Load new Song/Set/Session with a tempo other than 130bpm
**&rArr;** App and LinkHut tempo should both be 130bpm.

### TEMPO-4: Tempo range handling.

- Open LinkHut, press **Play**, when using QLinkHut click the **Link** button to enable
Link. - Open App, start Audio, and **enable** Link. - Change tempo in LinkHut to
**20bpm** **&rArr;** App and LinkHut should stay in sync. - Change Tempo in LinkHut to
**999bpm** **&rArr;** App and LinkHut should stay in sync. - If App does not support the
full range of tempos supported by Link, it should stay in sync by switching to a multiple
of the Link session tempo.

### TEMPO-5: Enabling Link does not change app's tempo if there is no Link session to join.
- Open App, start playing. - Change App tempo to something other than the default.
- **Enable** Link **&rArr;** App's tempo should not change. - Change App tempo to a new
value (not the default). - **Disable** Link **&rArr;** App's tempo should not change.

## Beat Time

These cases verify the continuity of beat time across Link operations.

### BEATTIME-1: Enabling Link does not change app's beat time if there is no Link session to join.
- Open App, start playing. - **Enable** Link **&rArr;** No beat time jump or
audible discontinuity should occur. - **Disable** Link **&rArr;** No beat time jump or
audible discontinuity should occur.

### BEATTIME-2: App's beat time does not change if another participant joins its session.
- Open App and **enable** Link. - Start playing. - Open LinkHut, when using QLinkHut
**enable** Link **&rArr;** No beat time jump or audible discontinuity should occur in the
App.

**Note**: When joining an existing Link session, an app should adjust to the existing
session's tempo and phase, which will usually result in a beat time jump. Apps that are
already in a session should never have any kind of beat time or audio discontinuity when
a new participant joins the session.

## Start Stop States

### STARTSTOPSTATE-1: Listening to start/stop commands from other peers.
- Open App, set Link and Start Stop Sync to **Enabled**.
- Open LinkHut and set Start Stop Sync to **Enabled**. When using QLinkHut click the **Link** button to enable
Link. Press **Play** **&rArr;** App should start playing according to its quantization.
- Stop playback in LinkHut **&rArr;** App should stop playing.

### STARTSTOPSTATE-2: Sending start/stop commands to other peers.
- Open LinkHut and set Start Stop Sync to **Enabled**. When using QLinkHut click the **Link** button to enable
Link. Press **Play**.
- Open App, set Link and Start Stop Sync to **Enabled** **&rArr;** App should not be
playing while LinkHut continues playing.
- Start playback in App **&rArr;** App should join playing according to its quantization.
- Stop playback in App **&rArr;** App and LinkHut should stop playing.
- Start playback in App **&rArr;** App and LinkHut should start playing according to
their quantizations.

## Audio Engine

These cases verify the correct implementation of latency compensation within an app's
audio engine.

### AUDIOENGINE-1: Correct alignment of app audio with shared session

 - Connect the audio out of your computer to the audio in. Alternatively use
[SoundFlower](https://github.com/mattingalls/Soundflower) to be able to record the output
of your app and LinkHut. - Open LinkHut, press **Play**, , when using QLinkHut click the
**Link** button to enable Link. - Open App and **enable** Link. - Start playing audio
(preferably a short, click-like sample) with notes on the same beats as LinkHut. - Record
audio within application of choice. - Validate whether onset of the sample aligns with
the pulse generated by LinkHut (tolerance: less than 3 ms).