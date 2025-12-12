# CV Dataset Capture

A single-file HTML app for rapidly capturing and organizing computer vision training images on mobile devices, with direct upload to Roboflow.

## Features

- **Progressive Web App (PWA)**: Install to home screen, works offline, fullscreen mode
- **Mobile-First Design**: Optimized for Android devices with touch-friendly controls
- **Rapid Capture**: Capture 50+ images in under 2 minutes
- **Crop Region Selection**: Desktop-first draggable crop box with aspect ratio presets
- **Batch Organization**: Group images into named batches before upload
- **Batch Management**: Rename batches in gallery, auto-generated batch names
- **Offline Storage**: Uses IndexedDB to store thousands of images locally
- **Image Optimization**: Optional automatic resize and compression
- **Direct Upload**: Upload batches directly to Roboflow with progress tracking
- **Quick Setup**: Paste any Roboflow URL to auto-fill workspace and project
- **Zero Dependencies**: Pure vanilla JavaScript, no frameworks or build tools
- **Privacy-First**: Your API keys stay in your browser, never sent to any third party

## Quick Start

### 1. Open the App

**Option A: Use GitHub Pages (Recommended)**
```
https://lockmeister.github.io/roboflow-dataset-capture/
```

**Option B: Install as Mobile App (Best Experience)**
1. Open the app URL in your mobile browser
2. Go to Settings (⚙️)
3. Tap **"📱 Install as Local App"**
4. Follow the browser prompts to install
5. Launch from your home screen like a native app!

**Benefits of Installing:**
- Appears on home screen with app icon
- Launches fullscreen (no browser UI)
- Faster access for field work
- Professional native app experience

**Option C: Run Locally**
```bash
# Clone or download this repo
cd roboflow-dataset-capture

# Serve with any static server, e.g.:
python -m http.server 8000

# Open http://localhost:8000 in your browser
```

### 2. Configure Roboflow Settings

**Option A: Quick Setup (Easiest)**
1. Tap the Settings icon (⚙️)
2. In **Quick Setup**, paste any Roboflow URL from your browser:
   - Your API settings page: `https://app.roboflow.com/experiments-pcvoe/settings/api`
   - Your project page: `https://app.roboflow.com/experiments-pcvoe/my-project`
   - Any other Roboflow page with your workspace/project
3. The app will automatically fill in Workspace ID and Project ID
4. Enter your **Private API Key** (the dotted one, not "rf_" key)
5. Toggle **Optimize Images** (recommended: ON)
6. Tap **Save Settings**

**Option B: Manual Entry**
1. Tap the Settings icon (⚙️)
2. Enter your **Private API Key** (Important: Use a Private key, NOT the Publishable key)
   - Get it from: https://app.roboflow.com/YOUR-WORKSPACE/settings/api
   - Look for "Private API Key" section (shown as dots •••, not the "rf_" key)
   - **Privacy Note:** Your key is stored locally in your browser only, never sent anywhere except directly to Roboflow when uploading
3. Enter your **Workspace ID** (e.g., `experiments-pcvoe` from your URL)
4. Enter your **Project ID** (e.g., `gesture-detection`)
5. Toggle **Optimize Images** (recommended: ON)
6. Tap **Save Settings**

### 3. Capture Images

1. Tap **New Batch**:
   - Quick option: Just press Enter to accept default name (`batch-1`, `batch-2`, etc.)
   - Custom name: Type your own (e.g., `thumbs-up`, `thumbs-down`)
   - **Note:** Spaces are NOT allowed - use dashes (`-`) or underscores (`_`) instead
   - Only letters, numbers, dashes, underscores, and dots are accepted
2. Point camera at subject
3. Tap the white capture button repeatedly
4. Batch name and image count displayed at top
5. Create additional batches as needed

### 3.5. Using Crop Mode (Optional)

**Perfect for desktop YouTube frame extraction with OBS Virtual Cam:**

1. Click the **✂️ Crop** button (bottom-left)
2. Crop overlay appears with draggable box
3. **Quick presets:**
   - **⬛ Off** - Turn off crop mode entirely
   - **✂️ Free** - Free-form crop (drag to any shape, no aspect ratio lock)
   - **□ 1:1** - Lock to square aspect ratio (1:1 for Instagram)
   - **📐 16:9** - Lock to landscape aspect ratio (16:9 for YouTube)
4. **Drag to move:** Click inside box and drag anywhere
5. **Resize:** Drag corner handles to resize
6. **Aspect ratio lock:** With Free mode, resize to any shape. With 1:1 or 16:9, resize maintains ratio
7. Only the cropped region will be captured

**Use Cases:**
- **YouTube videos:** Crop out UI, watermarks, subtitles via OBS Virtual Cam
- **Stationary camera:** Focus on specific area when camera is on tripod/stand
- **Screen recordings:** Extract specific regions from desktop recordings

### 4. Review and Upload

1. Tap the Gallery icon (📷)
2. Review captured images grouped by batch
3. **Rename batches**: Tap the blue "Rename" button to change batch names
4. **Delete images**: Tap the × on individual images to remove them
5. **Delete batches**: Tap the red "Delete" button to remove entire batches
6. Tap **Upload All** to send all batches to Roboflow
7. Monitor progress in the upload modal
8. **After upload:**
   - Click the link to view your images in Roboflow Annotate
   - Choose to delete uploaded batches or keep them locally
   - Images appear in the **Annotate** tab organized by batch name

### 5. Find Your Uploaded Images in Roboflow

Your images will be in: `https://app.roboflow.com/{workspace}/{project}/annotate`

- Look in the **Annotate** tab
- Images are organized by the batch name you specified
- Ready for annotation, training, or review

## Workflow Examples

### Mobile Camera Workflow
```
Open app
  ↓
New Batch "thumbs-up"
  ↓
Tap tap tap (50 photos in ~90 seconds)
  ↓
New Batch "thumbs-down"
  ↓
Tap tap tap (50 photos in ~90 seconds)
  ↓
Gallery → Delete 5 blurry shots
  ↓
Upload All → Wait 20 seconds
  ↓
Done! 95 images in Roboflow ready to annotate
```

### Desktop YouTube/OBS Virtual Cam Workflow
```
Set up OBS Studio
  ↓
Add Browser Source (YouTube video)
  ↓
Start Virtual Camera in OBS
  ↓
Open app in browser → Select OBS Virtual Camera
  ↓
Enable Crop mode (✂️) → Crop out YouTube UI
  ↓
Set aspect ratio (16:9 or Square)
  ↓
Play video in OBS, tap capture button for frames
  ↓
Upload batch to Roboflow
  ↓
Done! Perfect frame extraction from any video source
```

## Technical Details

### Architecture

- **Single HTML File**: Entire app is in `index.html` (HTML + CSS + JavaScript inline)
- **Storage**: IndexedDB for images (multi-GB capable), localStorage for settings
- **Camera**: Uses `getUserMedia()` API with rear camera preference
- **Image Processing**: Canvas API for client-side resize/compression
- **Upload**: Direct browser → Roboflow API via Fetch API

### Browser Compatibility

- **Recommended**: Chrome/Edge on Android
- **Requires**: Modern browser with camera access and IndexedDB support
- **Tested on**: Chrome 120+ (Android), Safari 17+ (iOS)

### Storage Limits

- **Typical**: 1000-2000 images per device (depends on browser quota)
- **Best Practice**: Upload batches frequently to free up space
- **Clearing Data**: Delete batches in Gallery or clear browser data for site

### Image Optimization

When enabled (default):
- Resizes to max 1024px on longest dimension
- Converts to JPEG with 80% quality
- Typical size: 200-400KB per image (from 2-4MB originals)
- Benefits: Faster uploads, lower Roboflow costs, meets recommended specs

### API Integration

The app uploads images using the Roboflow Upload API:

```
POST https://api.roboflow.com/dataset/{project}/upload
  ?api_key={your_key}
  &batch={batch_name}
  &name={filename}

Body: multipart/form-data with image file
```

**Note:** Only the project ID is required in the URL path. The workspace is used to construct the view URL only.

Each image is tagged with its batch name in Roboflow for easy organization.

**Where Images Are Stored:**
- Uploaded images appear in the **Annotate** tab of your Roboflow project
- If you specified a batch name, images will be in that batch
- Otherwise, they appear in the "uploaded via API" batch
- Images are ready for annotation, review, and model training
- Access them at: `https://app.roboflow.com/{workspace}/{project}/annotate`

## Privacy & Security

**Your data and credentials are completely safe:**

- **No Backend**: All processing happens in your browser - there is no server collecting your data
- **Local Storage Only**: Your API key is stored in your browser's localStorage, never transmitted to any third party
- **Direct to Roboflow**: Images upload directly from your browser to Roboflow's servers (no intermediary)
- **No Tracking**: No analytics, cookies, or third-party scripts
- **Open Source**: All code visible in `index.html` - audit it yourself anytime
- **No Secrets in Code**: The public repository contains no API keys or credentials (each user provides their own)

**Which API Key to Use:**
- Use a **Private API Key** (shown as •••••••••••••••••• in Roboflow settings)
- Do NOT use the Publishable API Key (the one starting with `rf_`)
- Publishable keys are only for client-side inference, not uploading
- Private keys are needed for uploading images to your dataset

**Why it's safe to use your Private key here:**
- Your key never leaves your browser except when making direct API calls to Roboflow
- This is the same security model as using Roboflow's own web interface
- If you're concerned, you can download the HTML file and audit all code before using

## Troubleshooting

### Camera not working
- Grant camera permissions when prompted
- Ensure you're using HTTPS (or localhost)
- Try a different browser
- Check if another app is using the camera

### Upload fails
- Verify API key in Settings is correct
- Check workspace and project IDs match your Roboflow account
- Ensure internet connection is active
- Check browser console for CORS errors (see below)
- Make sure the project exists in Roboflow (create it first if needed)

### Can't find uploaded images in Roboflow
- Go to: `https://app.roboflow.com/{workspace}/{project}/annotate`
- Click the **Annotate** tab in your project
- Look for your batch name in the sidebar
- Images might be in "uploaded via API" if batch name wasn't specified
- **Note:** The project must exist before uploading - create it in Roboflow first

### CORS errors
If direct API calls are blocked:
1. The app currently attempts direct browser → Roboflow uploads
2. If CORS blocks this, you'll need a proxy (Cloudflare Worker)
3. File an issue on GitHub if you encounter this

### Storage quota exceeded
- Upload and delete old batches
- Clear browser data for this site
- Use image optimization to reduce file sizes

### Images not appearing in gallery
- Refresh the gallery view
- Check browser console for errors
- Verify IndexedDB is enabled in browser settings

## Development

### File Structure
```
roboflow-dataset-capture/
  ├── index.html          # Complete app (HTML + CSS + JS)
  ├── README.md           # This file
  └── LICENSE             # MIT License
```

### Modifying the App

Since it's a single file:
1. Open `index.html` in your editor
2. HTML structure: `<body>` section
3. Styles: `<style>` section in `<head>`
4. JavaScript: `<script>` section before `</body>`
5. Save and refresh browser to test

### Key Functions

- `initDB()`: Sets up IndexedDB schema
- `initCamera()`: Requests camera access
- `capturePhoto()`: Captures frame, optimizes, saves to DB
- `uploadToRoboflow()`: Uploads all batches with progress
- `renderGallery()`: Displays all images by batch

## Roadmap (Future Features)

Not in MVP but possible additions:
- Video recording and frame extraction
- Auto-capture at intervals (like Roboflow Collect)
- PWA features (install to home screen, offline mode)
- Export batches as ZIP
- Cross-device sync via cloud storage
- CLIP-based image filtering
- Dark mode

## Contributing

This is an open-source tool. Contributions welcome:
- File issues for bugs or feature requests
- Submit PRs for improvements
- Share your use cases and feedback

## License

MIT License - see LICENSE file

## Credits

- Inspired by [Simon Willison's HTML Tools](https://simonwillison.net/2025/Dec/10/html-tools/)
- Built for the [Roboflow](https://roboflow.com) computer vision platform
- Created with Claude Code

## Support

- **Issues**: https://github.com/lockmeister/roboflow-dataset-capture/issues
- **Roboflow Docs**: https://docs.roboflow.com
- **Roboflow API**: https://docs.roboflow.com/api-reference/images/upload-api
