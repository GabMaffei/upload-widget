# Upload Widget

A React and TypeScript image-upload widget developed as a course-based learning project alongside Rocketseat's Tech Developer 360 coursework. This repository contains the frontend only; it expects a separately running upload API.

## Features in the current code

- Drag-and-drop and file-picker selection for multiple images.
- Upload progress, a pending-upload list, and a minimized widget state.
- Browser-side image conversion to WebP with optional dimension and quality limits.
- Download links for completed uploads.

The file picker accepts JPEG and PNG images. The upload client posts multipart form data to `http://localhost:3333/uploads` and expects a JSON response with a `url` field. That local API address is hard-coded in the source.

## Technology

React 19, TypeScript, Vite, Tailwind CSS, Zustand, Axios, React Dropzone, Motion, and Radix UI.

## Run locally

From this repository's root:

```bash
pnpm install
pnpm dev
```

Vite prints the local web address. To complete an upload, run a compatible backend on port `3333`; the related [upload-server](https://github.com/GabMaffei/upload-server) repository contains the API exercise.

## Current limitations

This repository has no backend or environment-variable configuration. Its upload client expects `{ "url": "..." }`, while the related API currently returns an empty `201` response. The frontend and API therefore need a response-contract change before the full upload flow can be considered integrated. No deployment or end-to-end verification is claimed here.
