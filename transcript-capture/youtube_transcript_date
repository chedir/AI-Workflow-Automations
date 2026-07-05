#!/usr/bin/python3

import os
import re
import sys
import subprocess
from youtube_transcript_api import YouTubeTranscriptApi

def extract_video_id(url):
    for pattern in [r"(?:v=|/)([0-9A-Za-z_-]{11})(?:[?&/]|$)", r"youtu\.be/([0-9A-Za-z_-]{11})"]:
        match = re.search(pattern, url)
        if match:
            return match.group(1)
    raise ValueError("Could not extract video ID from URL.")

def get_upload_date(url):
    result = subprocess.run(
        ["yt-dlp", "--print", "%(upload_date)s", "--skip-download", url],
        capture_output=True, text=True, check=True
    )
    raw = result.stdout.strip()
    if not re.fullmatch(r"\d{8}", raw):
        raise ValueError(f"Could not get upload date. Got: {raw}")
    return f"{raw[0:4]}-{raw[4:6]}-{raw[6:8]}"

def get_transcript_text(video_id):
    api = YouTubeTranscriptApi()
    fetched = api.fetch(video_id)
    return "\n".join(item.text for item in fetched)

def main():
    if len(sys.argv) != 4:
        print("Usage: python3 yt_transcript_rev2.py <youtube_url> <label> <outdir>")
        sys.exit(1)

    url = sys.argv[1]
    label = re.sub(r"\s+", "_", sys.argv[2].strip())
    label = re.sub(r"[^A-Za-z0-9_-]", "", label) or "transcript"
    outdir = sys.argv[3]

    os.makedirs(outdir, exist_ok=True)

    video_id = extract_video_id(url)
    print(f"Fetching upload date...")
    upload_date = get_upload_date(url)
    print(f"Fetching transcript...")
    transcript_text = get_transcript_text(video_id)

    filename = f"{upload_date}_{label}.txt"
    filepath = os.path.join(outdir, filename)

    with open(filepath, "w", encoding="utf-8") as f:
        f.write(transcript_text)

    print(f"Saved: {filepath}")

if __name__ == "__main__":
    main()
