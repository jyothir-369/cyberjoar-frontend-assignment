# Map Feature Editor

A web application for drawing and managing geometrical features (Polygon, Rectangle, Circle, Line String) on OpenStreetMap tiles with automatic polygon overlap handling and GeoJSON export functionality.

---

## Features

* 🗺️ **OpenStreetMap Integration**
  Renders OpenStreetMap tiles with smooth zooming and panning.

* ✏️ **Drawing Tools**
  Draw polygons, rectangles, circles, and line strings directly on the map.

* 🔒 **Non-Overlapping Polygons**
  Automatic overlap detection, trimming, and enclosure prevention for polygon-based features.

* 📤 **GeoJSON Export**
  Export all drawn features as a GeoJSON file.

* ⚙️ **Dynamic Configuration**
  Easily configurable limits for each feature type.

* 🎨 **Clean UI**
  Simple and intuitive interface with clear visual feedback.

---

## Tech Stack

* **React 18** with **TypeScript**
* **Vite** for build tooling
* **Leaflet** for map rendering
* **Turf.js** for spatial operations
* **Zustand** for state management

---

## Setup & Installation

### Prerequisites

* Node.js (v16 or higher)
* npm or yarn

### Installation Steps

1. **Clone the repository**

   ```bash
   git clone https://github.com/jyothir-369/cyberjoar-frontend-assignment.git
   cd cyberjoar-frontend-assignment
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Start the development server**

   ```bash
   npm run dev
   ```

4. **Open your browser**

   ```
   http://localhost:5173
   ```

---

## Build & Preview

### Build for production

```bash
npm run build
```

### Preview production build

```bash
npm run preview
```

---

## Usage

### Drawing Features

* Select a drawing tool from the toolbar:

  * **Polygon**: Click to add points, double-click to finish
  * **Rectangle**: Click and drag to define corners
  * **Circle**: Click to set center, drag to set radius
  * **Line String**: Click to add points, double-click to finish

### Drawing Rules

* **Polygon, Rectangle, Circle**

  * Cannot overlap existing polygon features
  * Overlapping areas are automatically trimmed
  * Fully enclosing another polygon is not allowed

* **Line String**

  * Not subject to overlap rules
  * Can freely cross other features

### Exporting

Click the **Export GeoJSON** button to download all drawn features.

---

## Configuration

### Maximum Shapes Per Type

Edit `src/config/index.ts`:

```ts
export const MAX_SHAPES_CONFIG: Record<string, number> = {
  polygon: 10,
  rectangle: 5,
  circle: 5,
  linestring: 20,
};
```

### Map Defaults

```ts
export const DEFAULT_MAP_CENTER: [number, number] = [20, 0];
export const DEFAULT_ZOOM = 2;
```

---

## Polygon Overlap Logic

Polygon overlap handling is implemented using **Turf.js** to ensure clean, non-overlapping geometries.

### Overlap Detection

* Uses `turf.intersect()` to detect shared areas
* Uses `turf.booleanContains()` to prevent full enclosure

### Auto-Trimming

* Overlapping areas are removed using `turf.difference()`
* If multiple polygons result, the largest valid polygon is kept
* Invalid or very small geometries are rejected

### Implementation Files

* `src/utils/polygonUtils.ts`
* `src/hooks/useDrawing.ts`

---

## Project Structure

```
src/
├── components/
│   ├── Map.tsx
│   ├── DrawingToolbar.tsx
│   └── ExportButton.tsx
├── hooks/
│   └── useDrawing.ts
├── store/
│   └── mapStore.ts
├── utils/
│   ├── polygonUtils.ts
│   └── geojsonExport.ts
├── types/
│   └── index.ts
├── config/
│   └── index.ts
└── App.tsx
```

---

## GeoJSON Export

* Standard GeoJSON `FeatureCollection`
* Each feature contains:

  * `geometry`
  * `id`
  * `type`
  * `color`

---

## Code Quality

* Strict TypeScript typing
* Modular architecture
* Well-documented spatial logic
* Graceful error handling and user feedback

---

## Browser Support

* Chrome / Edge (latest)
* Firefox (latest)
* Safari (latest)

---

## License

This project is created as part of a frontend development assignment.

---

## Deployment

The application can be deployed using:

* **Vercel**
* **Netlify**
* **GitHub Pages**

Example (Vercel):

```bash
npm install -g vercel
vercel --prod
```

---

## Future Enhancements

* Feature editing (move, resize, delete)
* Undo / Redo functionality
* Import GeoJSON support
* Feature styling options
* Additional map providers
