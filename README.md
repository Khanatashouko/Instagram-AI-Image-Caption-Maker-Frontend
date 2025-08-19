Instagram AI Caption Maker — Next.js Frontend & BLIP
[![Releases](https://img.shields.io/github/v/release/Khanatashouko/Instagram-AI-Image-Caption-Maker-Frontend)](https://github.com/Khanatashouko/Instagram-AI-Image-Caption-Maker-Frontend/releases)

Generate creative, human-like, SEO-friendly Instagram captions for images using BLIP and Google Gemini/Gemma. This Next.js frontend uploads images to a FastAPI backend and displays multiple caption styles.

Demo screenshot
![App demo screenshot](https://images.unsplash.com/photo-1520975910080-36d8b7b24c42?auto=format&fit=crop&w=1200&q=60)

Badges
- Topics: ai • blip • caption-generator • fastapi • gemini • gemma • instagram • nextjs • react • tailwindcss
- Releases: https://github.com/Khanatashouko/Instagram-AI-Image-Caption-Maker-Frontend/releases

Quick links
- Releases (download and run the release artifact): https://github.com/Khanatashouko/Instagram-AI-Image-Caption-Maker-Frontend/releases
- Source: this repository

Why this frontend
- Convert images into multiple caption styles: witty, professional, short, long, SEO-optimized.
- Combine BLIP vision encodings with Gemini/Gemma text generation for captions that respect image context.
- Ship a polished UI built with Next.js, React, and Tailwind CSS.
- Connect to a FastAPI backend that handles image processing, BLIP feature extraction, and calls to Gemini/Gemma.

Key features
- Upload images via drag-and-drop or file picker.
- Preview generated captions in multiple styles.
- Copy caption text and suggested hashtags.
- Edit captions inline and save favorites.
- Support for client-side image optimization and thumbnails.
- Responsive UI for mobile-first Instagram workflows.
- Simple environment config to point to your FastAPI backend.

Architecture overview
- Frontend: Next.js + React + Tailwind CSS. Client handles uploads, shows progress, and renders caption options.
- Backend: FastAPI (separate repo). Backend runs BLIP for vision, and forwards prompts/data to Gemini/Gemma.
- Flow: user uploads image -> frontend posts to backend -> backend returns multiple caption variants -> frontend renders list and actions.

Files you will find here
- pages/: Next.js page routes and API stubs.
- components/: UI components (Uploader, CaptionCard, Settings).
- styles/: Tailwind CSS config and custom styles.
- public/: Assets and demo images.
- README.md: this file.

Prerequisites
- Node.js 18+ (LTS recommended)
- npm, yarn, or pnpm
- Access to a FastAPI backend that exposes the expected upload and caption endpoints
- If running prebuilt release artifacts, download and execute the release file from the Releases page listed above.

Local development (frontend)
1. Clone
   git clone https://github.com/Khanatashouko/Instagram-AI-Image-Caption-Maker-Frontend.git
   cd Instagram-AI-Image-Caption-Maker-Frontend

2. Install
   npm install
   or
   pnpm install
   or
   yarn install

3. Environment
   Create a .env.local at project root with these variables:
   - NEXT_PUBLIC_API_URL=https://your-backend.example.com
   - NEXT_PUBLIC_MAX_UPLOAD_SIZE=5242880  # bytes (5 MB) default
   - NEXT_PUBLIC_DEFAULT_STYLE=creative

4. Run dev server
   npm run dev
   Visit http://localhost:3000

Production build
- Build
  npm run build
- Start
  npm run start

If you prefer Docker:
- Build image:
  docker build -t ig-caption-frontend .
- Run container:
  docker run -e NEXT_PUBLIC_API_URL=https://your-backend.example.com -p 3000:3000 ig-caption-frontend

Release artifacts
- Download and execute release file: https://github.com/Khanatashouko/Instagram-AI-Image-Caption-Maker-Frontend/releases
  The releases page contains packaged frontend builds and helper scripts. Download the matching artifact for your platform and run the included start script or binary to serve a prebuilt frontend. If the link does not load, check the Releases section on the repository page.

How the frontend talks to the backend
- POST /api/upload
  - Content-Type: multipart/form-data
  - Body: { file: image }
  - Response:
    {
      "image_id": "uuid",
      "thumbnail": "https://.../thumb.jpg",
      "status": "processing"
    }

- GET /api/captions?image_id=uuid&styles=creative,short
  - Response:
    {
      "image_id": "uuid",
      "captions": [
        {
          "style": "creative",
          "text": "Golden hour, cool vibes. Sunset paints the sky in coral and gold. #sunset #vibes",
          "score": 0.92,
          "hashtags": ["sunset","vibes"]
        },
        {
          "style": "short",
          "text": "Sunset mood. #goldenhour",
          "score": 0.87,
          "hashtags": ["goldenhour"]
        }
      ]
    }

- POST /api/save-favorite
  - Body: { image_id: "uuid", caption: "...", metadata: {...} }

Front-end responsibilities
- Validate file size and image type before upload.
- Show upload progress and result state.
- Render multiple captions and allow copy/edit actions.
- Provide simple hashtag suggestions based on caption text and image tags.
- Store favorites in localStorage or sync with backend when authenticated.

Caption styles implemented
- Creative: narrative, descriptive, uses sensory words.
- Short: concise, one-liner.
- Professional: brand-safe, polished.
- Hashtag-rich: includes optimized hashtags for reach.
- Emojis: emoji-enhanced variants for casual posts.
- SEO-optimized: includes keywords and call-to-action for profile growth.

Customization points
- Add or change caption styles in src/styles/captionStyles.js
- Swap BLIP prompts and Gemini prompt templates via backend config.
- Update suggested hashtag logic in components/HashtagGenerator.jsx
- Modify UI theme using tailwind.config.js and CSS variables

UI components of interest
- Uploader: drag-and-drop with preview, accepts multiple images.
- CaptionCard: renders a caption and actions (copy, edit, favorite).
- HashtagBar: shows suggested hashtags and allows one-click add.
- SettingsPanel: change backend endpoint, max size, default style.

Accessibility
- Buttons use accessible labels and keyboard focus.
- Images include alt strings generated from BLIP descriptions.
- Color contrast follows WCAG guidelines via Tailwind variables.

Testing
- Unit tests: Jest + React Testing Library for components.
- E2E: Playwright for flows (upload, generate captions, copy/save).
- Run tests:
  npm run test
  npm run test:e2e

Deployment
- Vercel: push to GitHub and set project to deploy with build command npm run build and output Directory .next
- Static hosting: export static build with next export and serve with any static host if you do not need server-side rendering.
- Docker: build and run container as shown above.

Authentication and user data
- The frontend supports optional auth. It ships with a simple token-based flow. If you enable auth, store tokens in secure cookie or localStorage and send Authorization: Bearer <token> on requests that save favorites.

Security tips
- Validate uploaded files on the backend.
- Enforce size and type limits client-side and server-side.
- Sanitize user input before persisting.

Contributing
- Fork the repo and open a feature branch.
- Keep commits small and focused.
- Follow the existing code style and lint rules.
- Open a pull request with a clear description and test steps.

Issue templates and PR checklist
- Report reproducible steps, expected vs actual behavior, environment.
- Attach screenshots or network logs when relevant.
- For PRs: include description, linked issue, and update changelog if user-visible changes exist.

Changelog and releases
- Check the Releases page for packaged builds and changelog: https://github.com/Khanatashouko/Instagram-AI-Image-Caption-Maker-Frontend/releases
- Download the matching artifact and run the included start script to deploy a prebuilt frontend.

License
- MIT License (modify as needed). See LICENSE file.

Acknowledgements
- BLIP for vision encoding.
- Google Gemini / Gemma for text generation.
- FastAPI for backend API patterns.
- Next.js and Tailwind CSS for UI and layout.
- Open-source contributors and community resources.

Contact
- Open issues on GitHub or submit pull requests to this repository.

Project topics
ai, blip, caption-generator, fastapi, gemini, gemma, instagram, nextjs, react, tailwindcss

Visual assets and icons
- Use Unsplash and free icon sets for UI mockups and placeholder content.
- Replace demo images with your own photos for testing results and caption tone.