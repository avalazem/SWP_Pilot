# Running the Experiment
# Note: All button presses only accept 'f' (all swp runs and visual/speech localizer)
# Note: Main-Exp and Localizer wait for 3 't's

# 1. Training
# 438 s total, 1 initial run w/ thorough instructions, 2 runs mimicking main-exp, 88 or 175 s each + instructions
# Run Instructions: 
cd training 

python swp_train_initial.py training_run_1.csv
python swp_train.py training_run_2.csv
python swp_train.py training_run_3.csv

cd .. 

# 2. Main-Exp
# 420 s each run; 42 min total - 5 s before first block,  4 blocks of 90 s w/ 15 s rest, 10 s after final block

# Run Instructions:
cd main-exp

python swp.py sub1_run_1.csv
python swp.py sub1_run_2.csv
python swp.py sub1_run_3.csv
python swp.py sub1_run_4.csv
python swp.py sub1_run_5.csv
python swp.py sub1_run_6.csv

cd ..

# 3. Localizer (all additionally have 2.0 s Merci after)
# Visual 222 s - 6 s before first block, 30 sec per block (30 s stim + 6 s rest), 6 s after last stim 
# Audio	 194 s - 2 s before first block, 16 s per block (10 s stim + 6 rest)
# Hand	 191 s - 5 s before first, 10 s per block, 6 s rest after
# Speech 191 s - 5 s before first, 10 s per block, 6 s rest after

# Run Instructions: 
cd localizer

python runVisualCategory.py --splash visual_categories/Instructions/Instructions.png
python audiovis.py --total-duration 194000 audio_categories/sub1_audio.csv
python audiovis.py --splash hand_categories/Instructions.png --total-duration 191000 hand_categories/sub1_hand.csv
python audiovis.py --splash speech_categories/Instructions.png --total-duration 191000 speech_categories/sub1_speech.csv
