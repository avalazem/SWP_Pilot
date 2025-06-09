# Single-Word Processing

# CHECKLIST SUJET_04
# - Assurez que tout fonctionne et que les câbles (en particulier pour les pressions sur le trigger et les boutons) sont branchés ☐
# - Assurez que les contrôleurs disposent de timings pour les TR. ☐
# - Expliquer l'aperçu et la motivation de l'expérience à sujet ☐
# - Demandez au participant s'il/elle est dactylo ou non (si oui faites le main-exp_type, main-exp_write sinon) ☐
# - Montrez-lui la tâche avec le tablette/clavier. ☐
# - Expliquez que répéter des mots et fredonner (pour le localisateur) sont mentaux! ☐
# - Les tâches de localisation sont après le signal! ☐
# - Expliquez au sujet et aux contrôleurs que le bouton gauche sera enfoncé après avoir répété le mot (doit être attaché avec du scotch) ☐
# - Commencez l'entraînement ☐
# - Commencez main runs ☐
# - Commencez le localisateur. Rappelez-lui les tâches du localisateur avant chaqun ☐
#   (il/elle doit appuyer sur le bouton quand il voit l'étoile, etc.)
# - Débriefing



# RUNNING THE EXPERIMENT
# Note: All button presses only accept 'f' (all swp runs and visual/speech localizer)
# Note: Main-Exp and Localizer wait for 3 't's

# 1. Training
# 1 initial run w/ thorough instructions, 1 run mimicking main-exp. Around 5 minutes total.
# Run Instructions:
cd training_write (Finger writing hand-runs)
cd training_type (Type hand-runs)

SDL_AUDIODRIVER=alsa python swp_train_initial.py training_run_1.csv
SDL_AUDIODRIVER=alsa python swp_train.py training_run_2.csv

cd .. 

# 2. Main-Exp
# 420 s each run; 42 min total - 5 s before first block,  4 blocks of 90 s w/ 15 s rest, 10 s after final block

# Run Instructions:
cd main-exp_write (Finger writing hand-runs)
cd main-exp_type (Type hand-runs)

SDL_AUDIODRIVER=alsa python swp.py sub4_run_1.csv
SDL_AUDIODRIVER=alsa python swp.py sub4_run_2.csv
SDL_AUDIODRIVER=alsa python swp.py sub4_run_3.csv
SDL_AUDIODRIVER=alsa python swp.py sub4_run_4.csv
SDL_AUDIODRIVER=alsa python swp.py sub4_run_5.csv
SDL_AUDIODRIVER=alsa python swp.py sub4_run_6.csv

cd ..

# 3. Localizer (all additionally have 2.0 s Merci after)
# Visual 222 s - 6 s before first block, 30 sec per block (30 s stim + 6 s rest), 6 s after last stim
# Hand and Speech tasks are done AFTER probe!!
# Audio	 194 s - 2 s before first block, 16 s per block (10 s stim + 6 rest)
# Hand	 209 s - 2 s before first, 11.5 s per block, 6 s rest after
# Speech 221 s - 2 s before first, 11.5 s per block, 6 s rest after

# Run Instructions: 
cd localizer

python runVisualCategory.py --splash visual_categories/Instructions/Instructions.png
SDL_AUDIODRIVER=alsa python audiovis.py --total-duration 194000 audio_categories/sub04_audio.csv
python audiovis.py --splash hand_categories/Instructions.png --total-duration 209000 hand_categories/sub04_hand.csv
python audiovis.py --splash speech_categories/Instructions.png --total-duration 221000 speech_categories/sub04_speech.csv


