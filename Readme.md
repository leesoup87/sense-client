# Cochlear.ai Sense (beta version)

## Getting Started

**Cochlear.ai** offers audio cognition systems as a service. Our cloud API service *Cochlear.ai Sense* enables developers to analyze audio contents by extracting non-verbal information. It is based on gRPC framework and python, java, node.js are supported in beta version.

If you need any help or support, please do not hesitate to send us an email at support@cochlear.ai.

Please send us the audio samples that are not working properly with our API and tell us any issues you face during the development. It would be greatly appreciated. Thank you for your participation!



### Available tasks

- File input methods
```
- 'speech_detector' (speech activity detection)
- 'music_detector' (music activity detection)
- 'age_gender' (age and gender detection)
- 'music_genre' (music genre detection)
- 'music_mood' (music mood estimation)
- 'music_tempo' (music tempo detection)
- 'music_key' (music key detection)
- 'event' (audio event detection)
```

- Streaming input methods
```
- 'speech_detector_stream' (speech activity detection)
- 'music_detector_stream' (music activity detection)
- 'age_gender_stream' (age and gender detection)
- 'music_genre_stream' (music genre detection)
- 'music_mood_stream' (music mood estimation)
- 'event_stream' (audio event detection)
```

For 'event' and 'event_stream', the following subtasks are available.
('babycry', 'carhorn', 'cough', 'dogbark', 'siren', 'snoring', 'glass')
In other cases, the subtask will be ignored.



## Quick Tutorial

In this short tutorial, we introduce *Cochlear.ai Sense* API and go through the process of analyzing your first audio content.



### Step 1. Get your Free API key
Every API access is managed with API key. If you are a first time user, visit http://cochlear.ai/beta-subscription/ to get your free API key.

All API keys are limited to 700 audio files and 10 minute audio streams per method per day. If you need extra quota, email support@cochlear.ai to get more quota with brief explanation.

```
Daily Quota : 700 calls per method (audio file) / 10 minutes per method (audio stream)
```


### Step 2. Clone this repository
This repository contains the libraries used for the *Cochlear Sense API* call. Download or copy to use.
```
git clone https://github.com/cochlearai/sense-client
```


### Step 3. Setup your environment (python)
This and the next steps assume the python 2.7 environment running on Ubuntu. If you are using java or node.js, please refer to the following documents:
(Java) https://github.com/cochlearai/sense-client/blob/master/JavaClient/Readme.md
(Node.js) https://github.com/cochlearai/sense-client/tree/master/NodeJS/Readme.md


#### Install portaudio
This is required only for streaming methods.
```
apt install portaudio19-dev
```


#### Install pip
Run the following codes.

```
wget https://bootstrap.pypa.io/get-pip.py
python get-pip.py
```
As an alternative, you can also use apt-get command
```
apt-get install python-pip
```
To install the dependencies presented below, pip version 10.0.1 or later is recommended.


#### (Optional) Install virtualenv
If you want to setup the python environment on virtualenv, run the following codes.

```
pip install virtualenv
virtualenv venv 
source venv/bin/activate
```
You can verify whether the virtual environment is successfully activated with the prefix *(venv)* in the terminal window.


#### Install python libraries
Run the following codes.
```
pip install --upgrade pip
pip install --no-cache-dir -r requirements.txt
```


### Step 4. Making your gRPC call

The predicted values are given in units of one second for all methods except for 'music_key' and 'music_tempo'. The size of the input audio file is recommended not to exceed but not limited to 100MB.

Note that the type of the result is not determined by the input audio but by the method you call. For example, if you call a music analysis method with a speech data, the model will regard the input as a music signal and make predictions based on its knowledge about the music. Please be aware of the kind of the audio inputs you are using.

#### Example

For the examples of  and , please refer ./examples/example.py and ./examples/example_streaming.py. (to be updated)
After inserting your API key to the example code, run the code below.
```bat
python ./examples/example.py
```



#### Example of Response

- Audio Event Detection

        {u'babycry': [0.884, 1.0, 0.126, 0.0, 0.0, 0.058, 0.416, 0.948, 0.782, 0.013]}
        
- Audio Music/Speech/Others (MSO) Classification

        {u'music': [0.0, 0.0, 0.0, 0.001, 0.001, 0.086, 0.0, 0.0, 0.001, 0.008],
         u'others': [1.0, 1.0, 1.0, 0.998, 1.0, 0.965, 1.0, 1.0, 1.0, 0.865],
         u'speech': [0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.004]}

- Speech Gender Detection and Classification

        {u'male': [0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0],
         u'female': [0.0, 0.0, 0.0, 1.0, 1.0, 0.257, 0.0, 0.0, 0.173, 0.935]}

- Music Key Estimation

        {u'key': u'Abm'}

- Music Tempo Estimation

        {u'tempo1': 128.571, u'tempo2': 42.857}
        
- Music Genre Classification

        {u’genre’: [u’Electronic’]}
        
- Music Mood Estimation

        {u'arousal': [-0.035, 0.058, -0.028, 0.22, 0.099, -0.038, -0.089, -0.049, 0.084, -0.01],
         u'valence': [0.01, 0.046, 0.006, 0.174, 0.068, 0.019, -0.01, -0.02, 0.092, -0.027]}




## Updating components in alpha testing

- HTTP referrers (REST API)
- Improvement on API Latency 
- Example client codes of other languages (C++, Java, Objective-c, cURL)
- Updated inference model
