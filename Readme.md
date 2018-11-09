# Cochlear.ai Sense (beta version)

## Getting Started

**Cochlear.ai** offers audio cognition systems as a service. Our cloud API service *Cochlear.ai Sense* enables developers to analyze audio contents by extracting non-verbal information. It is based on gRPC framework and python, java, node.js are supported in beta version.

If you need any help or support, please do not hesitate to send us an email at support@cochlear.ai.

Please send us the audio samples that are not working properly with our API and tell us any issues you face during the development. It would be greatly appreciated. Thank you for your participation!



### Available tasks

- File input methods

> 1. 'speech_detector' (speech activity detection)
> 2. 'music_detector' (music activity detection)
> 3. 'age_gender' (age and gender detection)
> 4. 'music_genre' (music genre detection)
> 5. 'music_mood' (music mood estimation)
> 6. 'music_tempo' (music tempo detection)
> 7. 'music_key' (music key detection)
> 8. 'event' (audio event detection)


- Streaming input methods

> 9. 'speech_detector_stream' (speech activity detection)
> 10. 'music_detector_stream' (music activity detection)
> 11. 'age_gender_stream' (age and gender detection)
> 12. 'music_genre_stream' (music genre detection)
> 13. 'music_mood_stream' (music mood estimation)
> 14. 'event_stream' (audio event detection)


For 'event' and 'event_stream', the following subtasks are available.

> 'babycry', 'carhorn', 'cough', 'dogbark', 'glassbreak', 'siren', 'snoring'

In other cases, the subtask will be ignored.

***

## Key features of beta version

Our beta version API includes the following major updates compared to the alpha version.

- Improved Latency
- Streaming input support
- Example client codes of other languages (Java, Node.js)
- Additional funcionalities
    - Speech and music activity detection
    - Age and gender detection
- Additional sound event class (glassbreak)
- Improved performance

***

## Quick Tutorial

In this short tutorial, we introduce *Cochlear.ai Sense* API and go through the process of analyzing your first audio content.



### Step 1. Get your Free API key
Every API access is managed with API key. If you are a first time user, visit http://cochlear.ai/beta-subscription/ to get your free API key.

All API keys are limited to 700 audio files and 10 minute audio streams per method per day.


> Daily Quota : 700 calls per method (audio file) / 10 minutes per method (audio stream)



### Step 2. Clone this repository
This repository contains the libraries required to utilize *Cochlear Sense API*. Copy with the code below or manually download to use.
```
$ git clone https://github.com/cochlearai/sense-client
```


### Step 3. Setup your environment (python)
This and the next steps assume the python 2.7 environment running on Ubuntu. If you are using java or node.js, please refer to the following documents:

(Java) https://github.com/cochlearai/sense-client/blob/master/JavaClient/Readme.md

(Node.js) https://github.com/cochlearai/sense-client/tree/master/NodeJS/Readme.md


- Install portaudio

This is required only for streaming methods.

```
$ apt install portaudio19-dev
```


- Install pip

Run the following codes.

```
$ wget https://bootstrap.pypa.io/get-pip.py
$ python get-pip.py
```

As an alternative, you can also use apt-get command

```
$ apt-get install python-pip
```

To install the dependencies presented below, pip version 10.0.1 or later is recommended.


- (Optional) Install virtualenv

If you want to setup the python environment on virtualenv, run the following codes.

```
$ pip install virtualenv
$ virtualenv venv 
$ source venv/bin/activate
```

You can verify whether the virtual environment is successfully activated with the prefix *(venv)* in the terminal window.


- Install python libraries

Run the following codes.

```
$ pip install --upgrade pip
$ pip install --no-cache-dir -r requirements.txt
```


### Step 4. Making your gRPC call

The predicted values are given in units of one second for all methods except for 'music_key' and 'music_tempo'. The size of the input audio file is recommended not to exceed but not limited to 100MB.

Note that the type of the result is not determined by the input audio but by the method you call. For example, if you call a music analysis method with a speech data, the model will regard the input as a music signal and make predictions based on its knowledge about the music. Please be aware of the kind of the audio inputs you are using.

- Example codes

For the examples of the file input methods and the streaming methods, please refer to ./examples/example.py and ./examples/example_streaming.py, respectively. (to be updated)

After inserting your API key to the example code, run the code below.

```
$ python ./examples/example.py
```

- Examples of Response (to be updated)

The following examples assume that the input is an audio file with a length of 3 seconds or an audio stream of 1 second.


##### 1. speech_detector
```
(file) {"speech": "speech", "probability": [0.662, 0.789, 0.515]}
(stream) {"speech": "speech", "probability": 0.662}
```
##### 2. music_detector
```
(file) {"music": "music", "probability": [0.662, 0.789, 0.515]}
(stream) {"music": "music", "probability": 0.662}
```
##### 3. age_gender
```
(file) [{"agender": "child", "probability": [0.856, 0.007, 0.031]}, 
        {"agender": "male", "probability": [0.115, 0.716, 0.703]}, 
        {"agender": "female", "probability": [0.029, 0.278, 0.266]}]
(stream) [{"agender": "child", "probability": 0.856}, 
          {"agender": "male", "probability": 0.115}, 
          {"agender": "female", "probability": 0.029}]
```
##### 4. music_genre
```
(file) {"genre": ["Rock", "Hip-hop", "Jazz"],  "probability": [0.616, 0.254, 0.112]}
(stream) {"genre": ["Rock", "Hip-hop", "Jazz"],  "probability": [0.616, 0.254, 0.112]}
```
##### 5. music_mood
```
{"arousal": 0.2952, "valence": -0.2254}
```
##### 6. music_tempo
```
(file) {"tempo": [72.0, 36.0], "probability": [0.881, 0.119]}
(stream) N/A
```
##### 7. music_key
```
(file) {"key": ["Gb"], "probability": 0.752}
(stream) N/A
```
##### 8. event
```
(file) {"event": ["babycry"],  "probability": [0.803, 0.911, 0.188]}
(stream) {"event": ["babycry"],  "probability": 0.803}
```
