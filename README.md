# 📱 TikTok Clone Bot

Automated bot that monitors a Telegram channel and publishes content to TikTok with translation from Italian to Spanish.

## 🎯 Features

- ✅ **Photo Posts**: Single photos converted to TikTok slideshow with translated captions
- ✅ **Photo Slideshows**: Multiple photos (2-35) with auto-generated music
- ✅ **Videos**: Videos with subtitles and translated captions
- ✅ **Auto Translation**: DeepL + OpenAI for high-quality translations
- ✅ **Subtitle Generation**: FFmpeg + Whisper for automatic Spanish subtitles
- ✅ **Error Handling**: Automatic retries with exponential backoff

## 📋 Requirements

- Python 3.11+
- FFmpeg (for subtitle generation)
- Telegram Bot
- Upload-Post.com account with TikTok connected
- API Keys: DeepL, OpenAI, HeyGen, CloudConvert, Groq

## 🚀 Setup

### 1. Clone Repository
```bash
git clone https://github.com/yourusername/tiktok-clone-bot.git
cd tiktok-clone-bot
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Configure Environment Variables

Copy `.env.example` to `.env` and fill in your API keys:
```bash
cp .env.example .env
```

Edit `.env` with your credentials:
```env
TELEGRAM_BOT_TOKEN=your_bot_token
SOURCE_CHANNEL_ID=-1003579454785
UPLOADPOST_API_TOKEN=your_uploadpost_token
UPLOADPOST_PROFILE=tiktok_profile
DEEPL_API_KEY=your_deepl_key
OPENAI_API_KEY=your_openai_key
GROQ_API_KEY=your_groq_key
HEYGEN_API_KEY=your_heygen_key
CLOUDCONVERT_API_KEY=your_cloudconvert_key
```

### 4. Run Locally
```bash
python main.py
```

## 🌐 Deploy to Railway

### 1. Create New Project

1. Go to [Railway.app](https://railway.app)
2. Click "New Project"
3. Select "Deploy from GitHub repo"
4. Choose your `tiktok-clone-bot` repository

### 2. Configure Environment Variables

In Railway dashboard, go to **Variables** and add:
```
TELEGRAM_BOT_TOKEN=your_bot_token
SOURCE_CHANNEL_ID=-1003579454785
UPLOADPOST_API_TOKEN=your_upload_post_token
UPLOADPOST_PROFILE=tiktok_profile
UPLOADPOST_API_URL=https://api.upload-post.com/api/upload
DEEPL_API_KEY=your_key
OPENAI_API_KEY=your_key
GROQ_API_KEY=your_key
HEYGEN_API_KEY=your_key
CLOUDCONVERT_API_KEY=your_key
SUBTITLE_FONT=Montserrat
SUBTITLE_FONT_SIZE=10
```

### 3. Deploy

Railway will automatically:
- Detect Python
- Install dependencies from `requirements.txt`
- Run `Procfile` command: `python main.py`

## 📊 How It Works

1. **Monitor**: Bot watches Telegram channel for new posts
2. **Download**: Downloads photos/videos from Telegram
3. **Process**:
   - Photos: Convert to TikTok slideshow with music
   - Videos: Convert to MP4 → Add Spanish subtitles
4. **Translate**: Caption IT → ES with DeepL + OpenAI
5. **Publish**: Upload to TikTok via Upload-Post API

## 🎨 Content Types

### Single Photo
```
Input: 1 photo + caption (Italian)
Output: TikTok slideshow (1 photo with music) + translated caption
```

### Photo Carousel
```
Input: 2-35 photos + caption (Italian)
Output: TikTok slideshow with auto-generated music + translated caption
```

### Video
```
Input: Video + caption (Italian)
Output: TikTok video with Spanish subtitles + translated caption
```

### Mixed Carousel (Photos + Videos)
```
Input: Photos + Videos + caption (Italian)
Output: 2 separate TikTok posts:
  - Slideshow with photos
  - Individual videos
```

## ⚙️ Configuration

Edit `config.py` to customize:

- `HEYGEN_TIMEOUT`: Max wait time for video translation (default: 600s)
- `CAROUSEL_WAIT_TIMEOUT`: Wait time for carousel items (default: 30s)
- `SUBTITLE_FONT_SIZE`: Subtitle text size (default: 10)
- `CAPTION_MAX_LENGTH`: Max caption length (default: 2200)
- `MAX_CAROUSEL_ITEMS`: Max photos in slideshow (default: 10)

## 🎥 TikTok-Specific Features

### Photo Slideshow
- Photos automatically converted to video slideshow
- Auto-generated music from TikTok library
- Optimized 9:16 aspect ratio

### Video Format
- Preferred aspect ratio: **9:16** (vertical)
- Duration: 10 seconds - 10 minutes
- Format: MP4 with H.264 codec

## 🐛 Troubleshooting

### Bot not receiving messages
- Ensure bot is added as admin to Telegram channel
- Check `SOURCE_CHANNEL_ID` is correct (use @userinfobot)

### Upload-Post errors
- Verify `UPLOADPOST_API_TOKEN` is valid
- Check TikTok account is connected in Upload-Post dashboard
- Ensure `UPLOADPOST_PROFILE` matches your TikTok profile name
- Go to User Management → Create Profile → Connect TikTok

### FFmpeg errors
- Install FFmpeg: `apt-get install ffmpeg` (Railway does this automatically)
- Check video format is supported

### Video translation takes too long
- HeyGen processing can take 5-10 minutes for long videos
- Adjust `HEYGEN_TIMEOUT` if needed

## 📝 API Services Used

- **Upload-Post**: TikTok publishing API
- **DeepL**: Primary translation service (IT → ES)
- **OpenAI**: Fallback translation + AI processing
- **Groq Whisper**: Fast audio transcription for subtitles
- **HeyGen**: Video translation with lip-sync
- **CloudConvert**: Video format conversion

## 🔗 Useful Links

- [Upload-Post Documentation](https://docs.upload-post.com)
- [TikTok Video Requirements](https://docs.upload-post.com/api/video-requirements)
- [Railway Deployment Guide](https://docs.railway.app)

## 📝 License

MIT

## 👨‍💻 Support

For issues, contact: gainhub1@gmail.com
