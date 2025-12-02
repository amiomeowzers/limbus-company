# Limbus Company - Avatar Creator

Website untuk membuat avatar custom milik Armina dari game Limbus Company, dengan fitur pemilihan background/environment.

## Fitur

- **Avatar Customization**: Customize berbagai aspek avatar termasuk:
  - Skin tone
  - Hair style & color
  - Eye color
  - Outfit
  - Accessories

- **Background/Environment Selection**: Pilih dari 6 environment berbeda:
  - Limbus Company Bus
  - The City
  - Limbus Office
  - Mirror Dungeon
  - Night Sky
  - Golden Bough

- **Additional Features**:
  - Randomize avatar untuk ide cepat
  - Export avatar configuration sebagai JSON
  - Responsive design untuk mobile & desktop
  - Live preview dengan background yang dipilih

## Tech Stack

- **SvelteKit** 2.49.0 (latest)
- **Svelte** 5.45.3 (latest)
- **TypeScript**
- **Vite** 7.2.2

## Development

```bash
# Install dependencies
npm install

# Start dev server
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open

# Build for production
npm run build

# Preview production build
npm run preview

# Type checking
npm run check
```

## Project Structure

```
limbus-company/
├── src/
│   ├── lib/
│   │   └── components/
│   │       └── AvatarCreator.svelte  # Main avatar creator component
│   ├── routes/
│   │   ├── +layout.svelte            # Layout with global styles
│   │   ├── +page.svelte              # Homepage
│   │   └── styles.css                # Global CSS variables
│   └── app.html                      # HTML template
├── static/                           # Static assets
└── package.json
```

## Usage

1. Kunjungi halaman utama
2. Pilih berbagai opsi customization untuk avatar
3. Pilih background/environment yang diinginkan
4. Gunakan tombol "Randomize" untuk randomize semua pilihan
5. Klik "Export" untuk download konfigurasi avatar sebagai JSON

## License

Created for Limbus Company fans by Armina
