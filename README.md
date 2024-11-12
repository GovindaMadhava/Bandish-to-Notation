# Bandish-to-Notation (Digital Audio Processing Lab, IIT-Bombay, under the mentorship of Prof. Preeti Rao)
Motivation:
The project addresses a unique challenge in Indian classical music where notation is inherently schematic and skeletal, serving primarily as a mnemonic device rather than a precise transcription. In Indian music traditions, notation consists of note sequences (sargam syllables) that provide an approximate guide to the melody, while the precise rhythmic placement and pitch- continuous realization are left to the performer based on their knowledge gained through oral transmission. This flexibility in interpretation, while culturally valuable, makes automatic transcription particularly challenging and interesting from a computational perspective.

Objective:
The primary goal was to develop a system that could automatically transcribe Indian classical vocal performances into schematic notation, particularly focusing on traditional compositions (bandishes) in North Indian Khayal style. This would help preserve evolving versions of traditional compositions and facilitate the notation of new compositions that exist only as recordings. The broader impact would enhance music pedagogy and expand the scope of raga music research by making vast audio resources more accessible for analysis.

Dataset Creation:
The first step of the project was to organize and process a dataset comprising compositions from two ragas belong to the Hindustani Yaman, Alhaiya Bilawal) and Carnatic Kalyani, Shankarabharana) traditions.
The dataset (~4 hrs/6GB) was meticulously structured to include 1520 compositions (kritis / bandishes) in each raga, with each set in different talas but all belonging to the same raga. These compositions were listed in the Data_Info Google Excel sheet. Subsequently, 35 artist renditions of each piece were sourced from YouTube, Kramik Pustak Malika(Hindustani Music Textbook) and other publicly available sources and recordings.
The original recordings often included accompanying instruments like violin, mridangam, tabla, and harmonium. To focus solely on the vocals, we sourced- separated the original recordings and obtained clean re-synthesized vocal files using the FTANet code. Pitch Contour plots for these recordings were generated using a Python notebook. Additionally, a metadata file was created for each audio track, containing information such as source, duration, tonic frequency/shruti, bpm, artist details, and rendered lyrics.
The data pre-processing pipeline included extracting pitch contours of source separated audio files usign Pitch Contour Detection (PCD) python script. The audios were then trimmed and audio-relevant info(artist name, link to source, time stamps, tonic frequency of recording, bpm, composition name) stored in a metadata file.
Hindustani bandish notations were sourced from the Bhatkhande textbook, and Carnatic notations from the official Karnataka Government prescribed Junior/Senior textbooks, the Library and Archives of Bangalore University.
Since the Hindustani notations were in Devnagari, a set of 28 symbols was devised to represent the swaras, octaves, silence, etc., essential for digitising the notation from paper to a digital(.csv) format along with lyrics and beats in the avartan/taal cycle.
My skills came in very handy as I helped manually notate each of the audios capturing rendition-specific notes and variations, which were digitised and aligned into the beat cycle. These were then verified and validated by expert musicians.

Methodology:
![Screenshot 2024-11-11 at 17.53.39.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/41c23b8e-74ea-499b-b84c-f5298716707d/f3e6c8e6-3825-4322-b765-bef8bbf176cc/Screenshot_2024-11-11_at_17.53.39.png) 

Model Training:
The model consists of single BiLSTM layer having 32 LSTM blocks followed by a fully connected layer with Softmax activation and Adam Optimizer with a learning rate of 0.001.
The output layer has 26 layers corresponding with our symbol set. Once the alignment of audio, lyrics, and notation was checked, the data was fed into the BiLSTM model, which was trained, tested, and validated.
Using tensorflow version 2.11.0 for our LSTM implementation, we were able to achieve:
56.82% accuracy for canonical notation prediction
50.16% accuracy for expert rendition-specific notation prediction

The findings of the project have been compiled into a research paper titled “SINGING TRANSCRIPTION WITH SCHEMATIC NOTATION FOR RAGA MUSIC“ and recieved encouraging feedback at The International Society for Music Information Retrieval (ISMIR) 2024 conference.
This project bridges the gap between oral tradition and computational analysis in Indian classical music, providing a detailed dataset (~4GB) with annotations and artist-specific notations for study and analysis. The model can also generate automatic sargam notations with lyrics and beat alignment, serving as a valuable tool for students to study and compare various artist renditions.
