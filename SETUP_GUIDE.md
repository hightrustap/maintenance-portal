# QR Maintenance Log System — Deployment Guide

## Files in This Package
| File | Purpose |
|------|---------|
| `inspector.html` | Mobile portal — scanned via QR code by workers |
| `admin.html` | Desktop admin dashboard — installable as PWA |
| `manifest.json` | Makes inspector.html installable on phones |
| `manifest-admin.json` | Makes admin.html installable on desktop |

---

## Step 1 — Host the Files

Upload all 4 files to any static web host. Free options:
- **GitHub Pages**: Push to a repo → Settings → Pages → Enable
- **Netlify**: Drag & drop the folder at netlify.com/drop
- **Vercel**: `npx vercel` from the folder
- **Any shared hosting**: Upload via FTP/cPanel to your domain

Example hosted URL: `https://workshop.yourcompany.com/`

---

## Step 2 — Generate QR Codes

Each machine has a unique URL:
```
https://YOUR-DOMAIN.com/inspector.html?machine=M01   ← CNC Lathe #1
https://YOUR-DOMAIN.com/inspector.html?machine=M02   ← CNC Lathe #2
... (M01 through M20)
```

To generate QR codes (free):
1. Go to https://qr-code-generator.com or https://www.qrcode-monkey.com
2. Paste each URL → Download PNG
3. Print and laminate each label
4. Affix to the corresponding machine

---

## Step 3 — Install the Admin Dashboard as Desktop App

### Chrome / Edge (Windows/Mac):
1. Open `admin.html` in Chrome or Edge
2. Click the install icon (⊕) in the address bar  
   OR go to: Menu (⋮) → "Install MaintenanceOS"
3. Click "Install" → it appears as a desktop shortcut

### To update later:
Simply update the hosted files — the PWA auto-refreshes.

---

## Step 4 — Inspector Mobile Setup (Optional)

Workers can also install the portal on their phone:
1. Scan any machine QR code
2. Browser shows "Add to Home Screen" prompt
3. Tap Add → appears as an app icon

---

## Machine IDs Reference

| ID | Machine | ID | Machine |
|----|---------|-----|---------|
| M01 | CNC Lathe #1 | M11 | Band Saw |
| M02 | CNC Lathe #2 | M12 | Radial Arm Drill |
| M03 | Milling Machine #1 | M13 | Turret Lathe |
| M04 | Milling Machine #2 | M14 | Air Compressor |
| M05 | Hydraulic Press | M15 | Overhead Crane |
| M06 | Power Press | M16 | Drill Press #1 |
| M07 | Surface Grinder | M17 | Drill Press #2 |
| M08 | Cylindrical Grinder | M18 | Sheet Metal Shear |
| M09 | Welding Station #1 | M19 | Bench Lathe |
| M10 | Welding Station #2 | M20 | Pneumatic Riveter |

---

## Customization

### Change machine checklists:
Edit the `MACHINES` object in `inspector.html` — each machine has its own array of checklist questions.

### Add real backend database:
Replace the `localStorage.setItem(...)` calls with `fetch()` calls to your own API (Node.js/Firebase/Supabase etc.).

### Add real authentication:
Integrate with your HR system's employee ID API to validate `empId` against a real employee database.

---

## Notes

- **Data storage**: Currently uses browser localStorage (shared between both files on the same domain). For production, connect to a cloud database.
- **Offline support**: Add a `sw.js` service worker for full offline capability.
- **Export**: Use the "Export CSV" button in the admin dashboard to download all records.
