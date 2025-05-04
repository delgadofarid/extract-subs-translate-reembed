# AI Video Subtitle Translator (English to Spanish)

This README contains complete instructions for generating Spanish subtitles for video files. When provided with this document and a video file, an AI assistant can efficiently complete the task without additional clarification.

## Task Overview

The task involves:
1. Extracting audio from a video file
2. Transcribing the audio to English text
3. Translating the transcription to Spanish
4. Embedding the Spanish subtitles back into the video

## Prerequisites

For the AI to execute this task, the user's system should have:

- FFmpeg installed
- Whisper AI installed
- Python 3.8+

## Complete Process for AI Execution

### Input

- Video file path provided by the user
- Optional output path (defaults to input_name_es.mp4)

### Step 1: Extract Audio from Video

The AI should run:
```bash
ffmpeg -i [INPUT_VIDEO] -q:a 0 -map a -c:a mp3 audio.mp3 -y
```

### Step 2: Transcribe Audio to English Text

The AI should run:
```bash
whisper audio.mp3 --model base --language en --output_format srt
```

This will generate an SRT file (audio.srt) with English subtitles.

### Step 3: Translate Subtitles to Spanish

The AI should:
1. Read the generated SRT file
2. Translate the text content while preserving timing and formatting
3. The AI should use its own translation capabilities to convert the subtitles from English to Spanish
4. When translating, the AI must preserve:
   - All subtitle numbers
   - All timestamp formats (00:00:00,000 --> 00:00:00,000)
   - Only translate the actual subtitle text
5. Save the translated content as spanish.srt

Example SRT format to preserve:
```
1
00:00:00,000 --> 00:00:07,000
[English text to translate to Spanish]

2
00:00:07,000 --> 00:00:16,000
[English text to translate to Spanish]
```

### Step 4: Embed Subtitles into Video

The AI should run:
```bash
ffmpeg -i [INPUT_VIDEO] -vf "subtitles=spanish.srt:force_style='FontSize=24,Alignment=2'" -c:a copy [OUTPUT_VIDEO] -y
```

### Step 5: Clean Up

Remove temporary files (audio.mp3, audio.srt, spanish.srt).

## Translation Guidelines for AI

When translating the subtitles, the AI should:

1. Maintain the meaning and tone of the original content
2. Adapt idioms and cultural references appropriately for Spanish-speaking audiences
3. Ensure proper Spanish grammar, spelling, and punctuation
4. Consider context across subtitle segments (maintain consistency in terms/names)
5. Properly handle dialogue markers, speaker identification, and non-verbal cues
6. For technical content, use domain-appropriate terminology in Spanish

## Output

A video file with embedded Spanish subtitles that:
- Maintains the original video and audio quality
- Has properly synchronized, readable Spanish subtitles
- Preserves the core message and tone of the original content

## Troubleshooting for AI

If the extraction or transcription steps fail:
- Check if the video file is valid and accessible
- Verify FFmpeg and Whisper are properly installed
- Try using a different audio format (e.g., WAV instead of MP3)

If the subtitle embedding fails:
- Verify the SRT file format is correct
- Check if the subtitle file is in the expected location
- Try adjusting the FFmpeg parameters for subtitle styling

## Example Execution for AI

```
1. Received video file: lecture.mp4
2. Extracted audio: ffmpeg -i lecture.mp4 -q:a 0 -map a -c:a mp3 audio.mp3 -y
3. Transcribed to English: whisper audio.mp3 --model base --language en --output_format srt
4. Translated subtitles from English to Spanish (preserving format)
5. Embedded subtitles: ffmpeg -i lecture.mp4 -vf "subtitles=spanish.srt:force_style='FontSize=24,Alignment=2'" -c:a copy lecture_es.mp4 -y
6. Returned lecture_es.mp4 with Spanish subtitles
```
