# CleanCut Engine

Backend for the CleanCut app. Takes an audio/video file (upload or link),
transcribes it with the Groq speech API, and silences or beeps foul language,
then returns a clean file. Runs ffmpeg + yt-dlp in a small container.

The user-facing page is hosted separately (Vercel, `cleancut-app`) and calls
this service's API.

- `POST /jobs` - multipart: `file` or `url`, `mode` (silence|beep), `tier`
- `GET /jobs/{id}` - status + flagged words
- `GET /jobs/{id}/download` - the cleaned file
- `GET /health` - liveness

## Env vars
- `GROQ_API_KEY` (required) - free key from console.groq.com
- `CLEANCUT_ALLOW_ORIGINS` - CORS allowlist (defaults to `*`)

Deploy: any Docker host. `render.yaml` is a ready Render blueprint (free plan).
