import requests
import json

def emotion_detector(text_to_analyze):
    # URL of the emotion analysis service
    url = 'https://sn-watson-emotion.labs.skills.network/v1/watson.runtime.nlp.v1/NlpService/EmotionPredict'

    # Constructing the request payload
    myobj = {
        "raw_document": {
            "text": text_to_analyze
        }
    }

    # Custom header specifying the model ID
    header = {
        "grpc-metadata-mm-model-id": "emotion_aggregated-workflow_lang_en_stock"
    }

    # Sending a POST request to the API
    response = requests.post(url, json=myobj, headers=header)

    if response.status_code == 200:
        # Parse the response from the API
        formatted_response = json.loads(response.text)

        anger_score = formatted_response['emotionPredictions'][0]['emotion']['anger']
        disgust_score = formatted_response['emotionPredictions'][0]['emotion']['disgust']
        fear_score = formatted_response['emotionPredictions'][0]['emotion']['fear']
        joy_score = formatted_response['emotionPredictions'][0]['emotion']['joy']
        sadness_score = formatted_response['emotionPredictions'][0]['emotion']['sadness']

        emotions = {
            'anger': anger_score,
            'disgust': disgust_score,
            'fear': fear_score,
            'joy': joy_score,
            'sadness': sadness_score
        }

        dominant_emotion = max(emotions, key=emotions.get)

    elif response.status_code == 400 or response.status_code == 500:
        anger_score = None
        disgust_score = None
        fear_score = None
        joy_score = None
        sadness_score = None
        dominant_emotion = None

    return {
        'anger': anger_score,
        'disgust': disgust_score,
        'fear': fear_score,
        'joy': joy_score,
        'sadness': sadness_score,
        'dominant_emotion': dominant_emotion
    }