# Availability Poster Generator

A single-page HTML tool for generating "Available Appointments" graphics for
Sunshine Healing and Massage Therapy. The output matches the existing template
(cream background, gold accents, script name, photo on the left) and can be
downloaded as a PNG suitable for posting to Facebook.

## Usage

1. Open `index.html` in a web browser. No server needed — everything runs
   locally.
2. Pick a staff member from the dropdown.
3. Add or edit the available time slots. Day comes from a dropdown, time is
   freeform text so you can enter things like `1:00 & 4:00` or `9:00-2:00`.
4. Click **Download PNG** to save a 2160×2700 image (rendered at 2× scale of
   the 1080×1350 design canvas).
5. Post the screenshot to Facebook.

## Adding or changing staff

Edit the `STAFF` array near the top of the `<script>` block in `index.html`:

```js
const STAFF = [
  { id: "ashley", name: "Ashley", photo: "photos/ashley.jpg" },
  { id: "sadie", name: "Sadie", photo: "photos/sadie.jpg" },
];
```

- `id` — a unique slug, used internally
- `name` — what shows up in the dropdown and as the big script heading
- `photo` — path to the photo, relative to `index.html`

Drop the actual photo files into the `photos/` directory. Portrait orientation
works best (the photo box on the poster is 580×760). The CSS uses
`background-size: cover` so any aspect ratio will be cropped to fit, but for
best results crop the photo to roughly 4:5 portrait before adding it.

## File layout

```
availability-poster/
├── index.html       # the whole app
├── photos/          # staff photos
│   ├── ashley.jpg
│   └── sadie.jpg
└── README.md
```

## Design notes

- Canvas: 1080×1350 (4:5 portrait, matches Instagram/Facebook portrait posts)
- Fonts: `Allura` (script), `Cormorant Garamond` (serif), `Inter` (sans)
- Colors:
  - Cream background `#F0E9D5`
  - Gold accent `#B5A063`
  - Ink text `#2F2F2F`

## Notes / limitations

- The script-style name renders with the `Allura` Google Font. The original
  template likely uses a slightly different (paid) script font, but `Allura`
  is a close free match.
- `html2canvas` is used for the PNG export. It runs entirely in the browser.
  External images load with `useCORS: true`, but since photos are served from
  the same directory as the HTML there should be no CORS issue.
- If the photo doesn't appear in the preview, check the browser console for
  404s and confirm the path in the `STAFF` config matches the file in
  `photos/`.
