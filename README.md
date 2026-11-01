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

## Source guide

| Source | What to inspect |
| --- | --- |
| [Widget composition](src/components/upload-widget.tsx) | Main upload interface. |
| [Upload state](src/store/uploads.ts) | Pending uploads and local state transitions. |
| [HTTP adapter](src/http/upload-file-to-storage.ts) | Multipart request, progress, and expected response. |
| [Image processing](src/utils/compress-image.ts) | Browser-side conversion/compression. |

## Integration contract

The request adapter sends a multipart upload to `http://localhost:3333/uploads`. A compatible API must return JSON containing the uploaded file's public `url` for the current client to use it. Successful file storage on the server and a successful client response are separate steps.

To review the frontend, follow file selection into the upload store, compression, the HTTP adapter, and the completed-upload item. The companion API's empty `201` response is a known contract gap; the README does not claim this full path is currently verified.
