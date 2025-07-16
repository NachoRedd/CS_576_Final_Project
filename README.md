# CS_576_Final_Project
Final Project For CS 576 Multimedia Systems by Ryan Li, Colbert Lin, and Jiaqi Wang
Utilizing https://docs.opencv.org/2.4/modules/highgui/doc/reading_and_writing_images_and_video.html


This project implements a video compression and decompression system with a focus on foreground/background segmentation.
The core idea is to apply different compression levels to moving objects (foreground) and static parts (background) of a video, allowing for qualitative improvement in foreground compression.
Key features and techniques used in this project include:
- Layer-based Compression:
  - The system separates video frames into foreground and background layers based on motion characteristics.
- Motion Detection and Segmentation:
  - Video frames are divided into 16×16 pixel macroblocks.
  - Motion vectors are computed for each macroblock based on the previous frame using Mean Absolute Difference (MAD)
  - Macroblocks are then classified as foreground or background based on the similarity and consistency of their motion vectors. Foreground blocks tend to have similar and contiguous motion vectors, while background blocks have near-zero or constant motion vectors.
- Differential Quantization:
  - After segmentation, 8x8 blocks within each macroblock undergo Discrete Cosine Transform (DCT) quantization.
  - DCT coefficients are quantized using different quantization step sizes n1 for the foreground and n2 for the background (typically n1 < n2, meaning we compress the background more) 
- Interactive A/V Player:
  - The decoder includes functionality to stop, pause, play, and step frame-by-frame through the video, allowing for detailed observation of the compressed and decompressed output.
- Additional Functionality:
  - The decoder utilizes multithreading to parallelize the parsing, dequantization of DCT coefficients, and reconstruction of video frames, allowing for synchronous decoding of RGB channels.


Example Usage with a foreground quantization of 2 and a background quantization of 4
<video width="50%" src="https://github.com/user-attachments/assets/23235f84-e86a-412f-b008-1dbf532e6b06"></video>

Example Usage with a foreground quantization of 0 and a background quantization of 7
<video width="100" src="https://github.com/user-attachments/assets/08e31fbf-7b2c-47f0-85b7-d25dd38b3758"></video>
