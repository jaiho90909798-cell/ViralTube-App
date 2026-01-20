# ViralTube-App
from moviepy.editor import VideoFileClip, AudioFileClip
from gtts import gTTS
import os

def dub_video(video_file, hindi_script, output_name):
    print("Step 1: Video load ho rahi hai...")
    clip = VideoFileClip(video_file)
    
    print("Step 2: Nayi dubbing voice ban rahi hai...")
    # Script ko audio mein badalna
    tts = gTTS(text=hindi_script, lang='hi')
    tts.save("temp_dub.mp3")
    
    print("Step 3: Audio aur Video ko joda ja raha hai...")
    new_audio = AudioFileClip("temp_dub.mp3")
    
    # Agar dubbing lambi hai toh video ko repeat ya adjust karna pad sakta hai
    # Yahan hum video ki length ke hisaab se audio set kar rahe hain
    final_clip = clip.set_audio(new_audio)
    
    print("Step 4: Final video save ho rahi hai...")
    final_clip.write_videofile(output_name, codec="libx264", audio_codec="aac")
    
    # Temporary file delete karna
    os.remove("temp_dub.mp3")
    print(f"Done! Aapki dubbed video '{output_name}' taiyar hai.")

# --- Istemal kaise karein ---
# Apni video ka sahi naam yahan likhein (e.g., 'my_video.mp4')
original_video = "input_video.mp4" 
nayi_script = "Namaste doston, is video mein humne naya voiceover dala hai."

dub_video(original_video, nayi_script, "dubbed_video_final.mp4")
