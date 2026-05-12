**Multimodal Emotion Recognition using Audio and Text**  
   
Aryansingh Sonaye   
AI25BTECH11032  
**Dataset**  
RAVDESS Emotional Speech Audio Dataset  
   
**Introduction**  
In this project, we worked on multimodal emotion recognition using both audio and text modalities. The main goal was to classify emotions from speech recordings using deep learning models.  
We used the RAVDESS dataset, which contains speech samples with different emotions like happy, sad, angry, fearful, surprised, etc.  
The project involved:  
- Audio preprocessing  
- Speech-to-text transcription  
- CNN model for audio  
- LSTM model for text  
- Early fusion  
- Late fusion  
- Evaluation using accuracy, precision, recall and F1-score  
   
**Dataset Description**  
The RAVDESS dataset contains emotional speech recordings from different actors.  
Emotions present in the dataset:  
- Neutral  
- Calm  
- Happy  
- Sad  
- Angry  
- Fearful  
- Disgust  
- Surprised  
The dataset mainly contains two spoken sentences:  
- “Kids are talking by the door”  
- “Dogs are sitting by the door”  
Because of this, the textual content has very limited variation.  
   
**Audio Preprocessing**  
For the audio modality:  
- Audio files were loaded using librosa  
- Mel spectrograms were generated  
- Spectrograms were resized and normalized  
- Spectrograms were used as CNN inputs  
For the bonus challenge, noise augmentation was also applied to the audio waveform before spectrogram generation.  
   
**Text Preprocessing**  
Speech-to-text transcription was generated using Whisper.  
The text data was then:  
- Tokenized  
- Converted into sequences  
- Padded to equal length  
These padded sequences were used as input to the LSTM model.  
   
**CNN Audio Model**  
The audio model used a Convolutional Neural Network (CNN).  
Architecture:  
- Conv2D  
- ReLU  
- MaxPooling  
- Conv2D  
- ReLU  
- MaxPooling  
- Fully Connected layers  
The CNN learned emotional features from mel spectrograms.  
   
**LSTM Text Model**  
The text model used:  
- Embedding layer  
- LSTM layer  
- Fully connected classifier  
The text sequences were converted into embeddings and passed through the LSTM to learn sequential information.  
However, because the dataset had only two sentences, the text model performed poorly.  
   
**Early Fusion Model**  
The early fusion model combined:  
- CNN audio features  
- LSTM text features  
Both feature vectors were concatenated and passed through fully connected layers for final emotion classification.  
This allowed the model to learn combined multimodal representations.  
   
**Late Fusion**  
Three late fusion methods were implemented:  
- Average fusion  
- Weighted fusion  
- Maximum-rule fusion  
The probabilities from CNN and LSTM models were combined during inference.  
Since the text model was weak, the late fusion results were mostly dominated by the audio model.  
   
**Architecture Diagram**  
Input Audio  
 ->  
 Mel Spectrogram Generation  
 ->  
 CNN Branch -> Audio Features  
 ->  
 Concatenation -> Fully Connected Layers -> Emotion Prediction  
 ->  
 LSTM Branch -> Text Features  
 ->  
 Tokenized Text Input  
Reasoning behind architecture:  
- CNN was used because spectrograms behave similarly to images.  
- LSTM was used because text is sequential data.  
- Fusion was used to combine information from both modalities.  
   
**Results Table**  
| | | |  
|-|-|-|  
| **Model** | **Accuracy** | **Weighted F1-score** |   
| LSTM Text Model | 0.09 | 0.04 |   
| CNN Audio Model | 0.61 | 0.61 |   
| Early Fusion Model | 0.62 | 0.62 |   
| Late Fusion Model | 0.64 | ~0.61 |   
   
   
**CNN Model Results**  
CNN Classification Report:  
- Accuracy: 0.61  
- Weighted F1-score: 0.61  
Observations:  
- CNN performed well on most emotions.  
- Calm and surprised emotions were detected relatively well.  
- Sad emotion was harder to classify correctly.  
- The model showed overfitting after several epochs since training accuracy reached 100%.  
   
**LSTM Model Results**  
LSTM Classification Report:  
- Accuracy: 0.09  
- Weighted F1-score: 0.04  
Observations:  
- The text model performed close to random guessing.  
- Most predictions collapsed into only a few classes.  
- This happened because the dataset contains only two textual statements, so there was almost no useful emotional information in text alone.  
   
**Fusion Model Results**  
Fusion Classification Report:  
- Accuracy: 0.62  
- Weighted F1-score: 0.62  
Observations:  
- Fusion slightly improved performance over the CNN model.  
- The audio modality dominated the predictions.  
- The text branch contributed very little useful information.  
- Fusion still helped slightly in some emotional classes.  
![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAnEAAAACCAYAAAA3pIp+AAAABmJLR0QA/wD/AP+gvaeTAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAANUlEQVR4nO3OQQ2AQBAAsSHhiQI0IWp9ngBsYIEfIWkVdJuZs5oAAPiLe6+O6vp6AgDAa+sBhYwEOqBD7p8AAAAASUVORK5CYII=)  
**Training and Validation Curves**  
The training curves showed:  
- CNN and Fusion models learned rapidly.  
- Both models eventually overfitted the training data.  
- LSTM model failed to learn meaningful emotional representations.  
The CNN and Fusion models reached nearly 100% training accuracy, while test accuracy saturated around 60–70%.  
   
**Bonus Challenge: Audio Augmentation**  
Noise augmentation was applied to the audio waveform before spectrogram generation.  
Small random Gaussian noise was added to improve robustness and reduce overfitting.  
After augmentation:  
- Training became slightly slower  
- Test accuracy reduced slightly  
- The experiment showed how augmentation affects emotional speech recognition models  
This happened because speech emotion recognition depends heavily on subtle acoustic patterns, which can get slightly distorted after adding noise.  
   
**Final Observations**  
Main observations from the project:  
- Audio features are much more useful than text features for the RAVDESS dataset.  
- CNN performed significantly better than the LSTM model.  
- Fusion worked, but gains were limited because the text modality was weak.  
- Emotion recognition in this dataset mainly depends on acoustic and prosodic speech information.  
   
**Conclusion**  
In this project, we implemented multimodal emotion recognition using audio and text modalities.  
The CNN audio model achieved the best overall performance and successfully learned emotional patterns from mel spectrograms. The LSTM text model performed poorly because the dataset contained very limited textual diversity.  
Early fusion slightly improved performance by combining audio and text features, while late fusion results were mostly dominated by the audio model outputs.  
Overall, the project demonstrated how multimodal deep learning models can be built for emotion recognition and also highlighted the importance of dataset characteristics when designing multimodal systems.  
![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAnEAAAACCAYAAAA3pIp+AAAABmJLR0QA/wD/AP+gvaeTAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAANUlEQVR4nO3OMQ2AABAAsSPBCj7fFjsymJHAjAU2QtIq6DIzW7UHAMBfnGt1V8fXEwAAXrsexNkF4H1/HJoAAAAASUVORK5CYII=)  
**Future Improvements**  
Possible future improvements:  
- Using transformer-based text models like BERT  
- Using larger emotion datasets  
- Applying stronger augmentation methods  
- Using attention-based fusion techniques  
- Reducing overfitting with better regularization  
