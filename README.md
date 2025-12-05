# -AI-Photo-Enhancer
Transform product photos with intelligent AI-powered natural language editing.

StatusNext.jsLicense

🎯 Quick Start
Prerequisites
Node.js 18+

API keys from:

Google Gemini

Replicate

OpenAI (optional)

Installation
bash
# Clone the repo
git clone https://github.com/yourusername/ai-photo-enhancer.git
cd ai-photo-enhancer

# Install dependencies
npm install

# Create environment file
cat > .env.local << 'EOF'
GEMINI_API_KEY=your_gemini_key
REPLICATE_API_KEY=your_replicate_key
OPENAI_API_KEY=your_openai_key
NEXT_PUBLIC_API_URL=http://localhost:3000
EOF

# Run locally
npm run dev
Visit http://localhost:3000

📋 Technical Write-Up
What It Does
AI Photo Enhancer transforms product photos using natural language commands. Users upload images, describe edits in plain English (e.g., "Remove background", "Add studio lighting"), and watch AI execute the transformations instantly with before/after comparison.

AI Models Used
1. Google Gemini Vision 2.0

Purpose: Analyze images and classify enhancement requests

Why chosen: Free tier (50 images/day), fast response (~2s), excellent image understanding capabilities

Usage: Processes user prompts to determine which AI model to route to

2. Replicate API (Community Models)

Purpose: Execute specialized image transformations

Models used:

rembg: Intelligent background removal with edge preservation

GFPGAN: Face/image restoration and color enhancement

SDXL: Style transfer and creative enhancements

Why chosen: Production-tested, cost-effective ($0.001/prediction), modular architecture

3. OpenAI DALL-E 3 (Optional)

Purpose: Generate product variations from descriptions

Why chosen: Highest quality outputs for professional results ($0.04/image)

Architecture
text
Frontend (React/Next.js)
    ↓
Upload Image → FileReader converts to Base64
    ↓
POST /api/enhance-image
    ↓
Gemini Vision analyzes prompt & classifies edit type
    ↓
Route to appropriate model:
├─ "Remove background" → Replicate rembg
├─ "Lighting/brightness" → Replicate SDXL
├─ "Colors/enhance" → Replicate GFPGAN
└─ "Custom prompt" → Replicate SDXL
    ↓
Image processing returns enhanced URL
    ↓
Display side-by-side before/after
    ↓
Store in edit history (client-side)
    ↓
Download enhanced image as JPEG
Major Components
Frontend

Drag-drop upload area with file validation

Real-time before/after side-by-side preview

4 quick-effect preset buttons

Natural language text input

Edit history sidebar with timestamps

Responsive design (mobile & desktop)

Backend

Next.js API Routes for serverless execution

Input validation (image size <5MB, prompt sanitization)

Error handling with user-friendly messages

Environment variable management for API keys

Integration Points

lib/gemini.ts: Handles Gemini Vision API calls

lib/replicate.ts: Routes to appropriate image models

lib/dalle.ts: Optional DALL-E variant generation

lib/imageUtils.ts: Base64 conversion, validation

Tech Stack
Layer	Technology
Frontend	Next.js 14, TypeScript, Vanilla CSS
Backend	Next.js API Routes
AI Integration	Gemini Vision 2.0, Replicate, OpenAI
Deployment	Vercel (serverless)
Storage	None (images processed on-the-fly)
Key Features
✅ Natural Language Interface - Describe edits conversationally
✅ Smart Model Routing - Gemini classifies prompts to optimal AI service
✅ Real-time Preview - Instant before/after comparison
✅ Edit History - Track all transformations with timestamps
✅ Production-Ready - Error handling, validation, security
✅ Cost-Efficient - Free tier + $5/month free credits
✅ Fully Deployed - Live on Vercel with working demo

Use Cases
E-commerce sellers: Enhance product listings automatically

Influencers: Quick photo touchups for social media

Product photographers: Batch enhancement without Photoshop

Small businesses: Professional photos on limited budget

Pricing
Service	Free Tier	Cost
Gemini Vision	50 images/day	$0
Replicate	$5 monthly credits	$0.001/prediction
DALL-E	Optional	$0.04/image
Monthly Total	~$0	up to $5
How to Test
Live Demo: ai-photo-enhancer.vercel.app

Click "Use Demo Image"

Try prompts like:

"Remove background"

"Add professional lighting"

"Enhance colors and saturation"

"Add depth and shadow"

Download your enhanced image

Deployment
