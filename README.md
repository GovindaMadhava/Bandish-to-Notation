# Bandish-to-Notation (MusicTech Research Internship @Digital Audio Processing Lab, IIT-Bombay, under the mentorship of Prof. Preeti Rao -> Dec '23 - Apr '24)

Motivation:
The project addresses a unique challenge in Indian classical music where notation is inherently schematic and skeletal, serving primarily as a mnemonic device rather than a precise transcription. In Indian music traditions, notation consists of note sequences (sargam syllables) that provide an approximate guide to the melody, while the precise rhythmic placement and pitch- continuous realization are left to the performer based on their knowledge gained through oral transmission. This flexibility in interpretation, while culturally valuable, makes automatic transcription particularly challenging and interesting from a computational perspective.

Objective:
The primary goal was to develop a system that could automatically transcribe Indian classical vocal performances into schematic notation, particularly focusing on traditional compositions (bandishes) in North Indian Khayal style. This would help preserve evolving versions of traditional compositions and facilitate the notation of new compositions that exist only as recordings. The broader impact would enhance music pedagogy and expand the scope of raga music research by making vast audio resources more accessible for analysis.

Dataset Creation:
The dataset comprises compositions from two ragas belonging to the Hindustani(Yaman, Alhaiya Bilawal) and Carnatic(Kalyani, Shankarabharana) traditions.
The dataset(~4 hrs/6GB) was meticulously structured to include 15-20 compositions (kritis / bandishes) in each raga, with multiple artists rendering the same piece.
The original recordings often included accompanying instruments like violin, mridangam, tabla, and harmonium which had to be source-separated, re-synthesized and pitch contours checked.
Metadata file containing audio relevant info such as source, duration, tonic frequency/shruti, bpm, artist details, and rendered lyrics were attached
Since the Hindustani notations were in Devnagari, a set of symbols was devised to represent the swaras, octaves, silence, etc., essential for digitising the notation from paper to a digital(.csv) format along with lyrics and beats in the avartan/taal cycle.
My skills came in very handy as I helped manually notate each of the audios capturing rendition-specific notes and variations, which were digitised and aligned into the beat cycle. These were then verified and validated by expert musicians.

![16 notes.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/41c23b8e-74ea-499b-b84c-f5298716707d/d9fec7db-6b20-4d32-a273-8fc545bb321e/16_notes.png)
<Set of 16 symbols used in the script digitization process>

![Screenshot 2024-11-11 at 17.54.56.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/41c23b8e-74ea-499b-b84c-f5298716707d/c6e411d9-1477-4204-be49-8c2c8d49cf91/Screenshot_2024-11-11_at_17.54.56.png)
<Summary of the dataset>

![Screenshot 2024-11-11 at 13.49.27.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/41c23b8e-74ea-499b-b84c-f5298716707d/94c99188-a609-4368-a171-36f9c0290d5b/Screenshot_2024-11-11_at_13.49.27.png)
<An image of a Bhatkhande bandish notation>

![Screenshot 2024-11-11 at 13.48.34.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/41c23b8e-74ea-499b-b84c-f5298716707d/e40ff841-6bd8-4fd5-9b96-6328379b5996/Screenshot_2024-11-11_at_13.48.34.png)
<Digitized csv notation of above Bhatkhande notation with swara, lyrics and taal/beat cycle in Devanagari>

![Screenshot 2024-11-11 at 17.42.33.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/41c23b8e-74ea-499b-b84c-f5298716707d/746e6f9e-808c-472c-85bd-1110f9a8bd1e/Screenshot_2024-11-11_at_17.42.33.png)
<csv notation of a Carnatic Music kriti containing the swara/notes, sahitya/lyrics and tala cycle in English>

Methodology:
![Screenshot 2024-11-11 at 17.53.39.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/41c23b8e-74ea-499b-b84c-f5298716707d/f3e6c8e6-3825-4322-b765-bef8bbf176cc/Screenshot_2024-11-11_at_17.53.39.png)
<Diagrammatic represesntation of the project pipeline>

![Screenshot 2024-11-11 at 17.52.10.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/41c23b8e-74ea-499b-b84c-f5298716707d/8dfdd767-0692-4b0b-a9c1-e753bafbcdb6/Screenshot_2024-11-11_at_17.52.10.png)
![Screenshot 2024-11-11 at 17.53.56.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/41c23b8e-74ea-499b-b84c-f5298716707d/03a2745e-900e-43bc-900a-92a6cae70364/Screenshot_2024-11-11_at_17.53.56.png)
![Screenshot 2024-11-11 at 17.52.41.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/41c23b8e-74ea-499b-b84c-f5298716707d/44435cd0-edcb-4001-8967-06a9cea9daf0/Screenshot_2024-11-11_at_17.52.41.png)
<Median-value based notation evaluation>

Model Training: 
The model consists of single BiLSTM layer having 32 LSTM blocks followed by a fully connected layer with Softmax activation and Adam Optimizer with a learning rate of 0.001.

![Network_Blk_Diag_new.svg](https://prod-files-secure.s3.us-west-2.amazonaws.com/41c23b8e-74ea-499b-b84c-f5298716707d/2d52bd20-e076-486e-bfc3-bccd09ec5dc4/Network_Blk_Diag_new.svg)
<Flow Chart depicting the model architecture>

The output layer has 26 layers corresponding with our symbol set. Once the alignment of audio, lyrics, and notation was checked, the data was fed into the BiLSTM model, which was trained, tested, and validated.

The model achieved:
- 68.82% accuracy for canonical notation prediction
- 60.16% accuracy for expert rendition-specific notation prediction

![Screenshot 2024-11-11 at 17.48.58.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/41c23b8e-74ea-499b-b84c-f5298716707d/ecc2066c-4d2f-4050-81d8-716bbe5d17c3/Screenshot_2024-11-11_at_17.48.58.png)
![Screenshot 2024-11-11 at 17.49.27.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/41c23b8e-74ea-499b-b84c-f5298716707d/98180359-984f-4c9f-b22e-a262a646c1cd/Screenshot_2024-11-11_at_17.49.27.png)

The findings of the project have been compiled into a research paper titled “SINGING TRANSCRIPTION WITH SCHEMATIC NOTATION FOR RAGA MUSIC“. We plan to increase the dataset size which would improve the performance, to be submitted at The International Society for Music Information Retrieval (ISMIR) 2025 conference.

This project bridges the gap between oral tradition and computational analysis in Indian classical music, providing a detailed dataset (~4GB) with annotations and artist-specific notations for study and analysis. The model can also generate automatic sargam notations with lyrics and beat alignment, serving as a valuable tool for students to study and compare various artist renditions.

Skills: Python, Music Transcription, Machine Learning, Audio Source Separation, Dataset creation, Audio Tagging
