# SMART ADR Connect

[![Vue.js](https://img.shields.io/badge/Vue.js-3.x-4FC08D?logo=vue.js)](https://vuejs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?logo=typescript)](https://www.typescriptlang.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.x-38B2AC?logo=tailwind-css)](https://tailwindcss.com/)
[![Google Apps Script](https://img.shields.io/badge/Backend-Google_Apps_Script-4285F4?logo=google)](https://developers.google.com/apps-script)

**SMART ADR (Adverse Drug Reaction)** is a serverless Progressive Web Application (PWA) designed to facilitate the reporting and tracking of drug allergies. Developed to address gaps in off-hour reporting and proactive prevention, this tool allows healthcare professionals to search for patient allergy history and submit new ADR reports instantly via a mobile-friendly interface.

## Key Features

*   **Patient History Search:** Instantly search for drug allergy history using Hospital Number (HN) or Citizen ID (CID).
*   **Proactive Reporting:** A streamlined form for reporting Adverse Drug Reactions (ADR).
*   **Naranjo Algorithm Calculator:** Built-in interactive tool to assess the probability of the ADR.
*   **Mobile-First Design:** Optimized for mobile use by nurses and pharmacists on rounds.
*   **Serverless Architecture:** Powered by Google Sheets and Google Apps Script for zero-cost infrastructure and ease of maintenance.

## Tech Stack

*   **Frontend Framework:** Vue.js 3 (Composition API)
*   **Language:** TypeScript
*   **Build Tool:** Vite
*   **Styling:** Tailwind CSS (v3)
*   **Icons:** Lucide Vue
*   **Backend / API:** Google Apps Script (GAS)
*   **Database:** Google Sheets

## Getting Started

Follow these instructions to set up the project on your local machine for development.

### Prerequisites

*   **Node.js** (v16.0.0 or higher)
*   **npm** or **yarn** or **bun**
*   A **Google Account** (for hosting the database and backend script)

---

### 1. Backend Setup (Google Sheets & GAS)

Since this project uses Google Sheets as a database, you must set it up first.

1.  Create a new **Google Sheet**.
2.  Rename the spreadsheet (e.g., `SmartADR_DB`).
3.  Create two tabs (Sheets) with the exact following names and headers:
    *   **Tab 1: `SmartADR_Reports`** (For storing new reports)
        *   *Columns:* `hn`, `timestamp`, `agent`, `symptom`, `reporter`, `note`, `naranjo_result`, `patient_cid`
4.  Go to **Extensions > Apps Script**.
5.  Paste the backend code (from `Code.gs`) into the editor.
6.  **Update the `SHEET_ID`** constant in the script with your Google Sheet ID (found in the URL).
7.  Click **Deploy > New deployment**.
    *   **Select type:** Web app.
    *   **Execute as:** Me.
    *   **Who has access:** **Anyone** (Critical for the frontend to access the API).
8.  Copy the generated **Web App URL**.

---

### 2. Frontend Setup

1.  **Clone the repository**
    ```bash
    git clone https://github.com/suradet-ps/smart-adr.git
    cd smart-adr
    ```

2.  **Install dependencies**
    ```bash
    bun install
    ```

3.  **Configure Environment**
    Open `src/App.vue` (or create a `.env` file if configured) and replace the API URL with your Google Web App URL from the backend setup step.

    ```typescript
    // src/App.vue
    const API_URL = 'https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec';
    ```

4.  **Run the development server**
    ```bash
    bun run dev
    ```

5.  Open your browser and navigate to `http://localhost:5173` (or the port shown in your terminal).

## Project Structure

```text
smart-adr/
├── public/              # Static assets
├── src/
│   ├── components/      # Vue components
│   │   ├── SearchPanel.vue  # Search interface component
│   │   └── ReportForm.vue   # ADR reporting form component
│   ├── assets/          # Images and styles
│   ├── App.vue          # Main application layout
│   ├── main.ts          # Entry point
│   ├── style.css        # Global styles & Tailwind directives
│   └── types.ts         # TypeScript interfaces
├── .gitignore
├── index.html
├── package.json
├── tailwind.config.js   # Tailwind configuration
└── tsconfig.json
```

## Build for Production

To create a production-ready build:

```bash
bun run build
```

The output will be in the `dist` directory, which can be deployed to any static hosting service (Vercel, Netlify, Firebase Hosting, or GitHub Pages).

## Contributing

Contributions are welcome! Please follow these steps:

1.  Fork the project.
2.  Create your Feature Branch (`git checkout -b feature/AmazingFeature`).
3.  Commit your changes (`git commit -m 'Add some AmazingFeature'`).
4.  Push to the Branch (`git push origin feature/AmazingFeature`).
5.  Open a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
