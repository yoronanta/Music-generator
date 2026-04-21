# AI Music Generator

This project uses a Long Short-Term Memory (LSTM) neural network to generate music in MIDI format. The model is trained on a dataset of MIDI files (primarily from video game soundtracks) and learns to predict sequences of notes and chords. Since I worked on it quite a long ago, some used libraries are outdated. Some examples of output music are attached below. It's interesting, that best pieces were created using Final Fantasy VII music datasets. I believe this stems from how naturally retro game music can be maped to MIDI. Also you can mention heavy bass notes in attached samples, this is a unique feature of FFVII dataset as well.

## How It Works

1. **Data Preparation**: The script scans the `midi_songs/` directory for `.mid` files.
2. **Feature Extraction**: Using the `music21` library, each MIDI file is parsed to extract notes and chords.
3. **Sequence Creation**: The extracted notes are converted into sequences of integers, where each integer represents a unique pitch or chord.
4. **Model Training**: An LSTM network is trained to predict the next note in a sequence given the previous 100 notes.
5. **Music Generation**: After training, the model can generate new sequences of notes, which are converted back to MIDI format.

## Dependencies

- Python 3.x
- Libraries:
  - glob
  - pickle
  - numpy
  - music21
  - keras
  - tensorflow

Install dependencies using pip:
```bash
pip install numpy music21 keras tensorflow
```

## Usage

1. Place your MIDI files in the `midi_songs/` directory.
2. Run the training script:
   ```bash
   python lstm.py
   ```
3. The script will:
   - Parse all MIDI files in `midi_songs/`
   - Save the extracted notes to `data/notes` (a pickle file)
   - Train the LSTM model and save checkpoints to the current directory (e.g., `weights-improvement-XX-XXXX-bigger.keras`)
4. To generate music, you would need to use the trained model (this script focuses on training; generation code would be similar to other LSTM music generation examples).

## Notes

- The script creates a `data/` directory to store the processed notes. If it doesn't exist, the script will attempt to create it when saving the notes.
- Training requires a significant amount of time and computational resources, especially with a large dataset of MIDI files.
- The model architecture consists of three LSTM layers with dropout and batch normalization for regularization.
- The MIDI files in the `midi_songs/` directory are used as the training dataset. Feel free to add your own `.mid` files to expand the dataset.

## Example MIDI Files

The `midi_songs/` directory includes a variety of MIDI files, primarily from video game soundtracks (e.g., Final Fantasy, Kingdom Hearts, Zelda). These provide a diverse training set for the model to learn musical patterns.

## Troubleshooting

- If you encounter an error about missing directories, ensure the `data/` directory exists or that the script has permission to create it.
- Make sure all MIDI files are valid and not corrupted.
- If you encounter memory issues, consider reducing the batch size or the number of LSTM units.

## License

This project is open source and available for modification and distribution.
