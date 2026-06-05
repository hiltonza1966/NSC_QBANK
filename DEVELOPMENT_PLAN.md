# NSC QBank - Updated Development Plan
**Aligned to Current System | 4 June 2026**

## Current State (Verified Today)
✅ Backend running on http://localhost:4000
✅ /api/export/health returns 200
✅ Pandoc export service implemented (src/export.ts)
✅ CORS configured for http://localhost:5173
✅ Rate limiting active

## Phase 1 - COMPLETE
- Express server with TypeScript
- /api/export route mounted
- Health check working

## Phase 2 - NEXT (This Week)
### 2.1 Frontend Export Buttons
Create: frontend/src/components/ExportButtons.tsx
- Wire to POST http://localhost:4000/api/export
- Use your v4 design system (.btn-primary)
- Support PDF, DOCX, HTML

### 2.2 Paper Builder Integration
- Take markdown from your Papers page
- Pass to export endpoint
- Download with proper filename: NSC-Maths-P1-2024.pdf

### 2.3 Bilingual Support
- Add language toggle (EN/AF)
- Pass to Pandoc with --metadata lang

## Phase 3 - Database Integration
### 3.1 Prisma Schema
```prisma
model Question {
  id        String @id @default(cuid())
  subject   String
  grade     Int
  topic     String
  language  String @default("en")
  markdown  String @db.Text
  marks     Int
  year      Int?
  createdAt DateTime @default(now())
}
```

### 3.2 API Routes
- GET /api/questions?subject=Mathematics&grade=12
- POST /api/papers/generate
- POST /api/papers/:id/export

## Phase 4 - DBE Features
- CAPS taxonomy tagging
- Memo generation (separate export)
- Moderation workflow
- Bulk import from Word

## File Structure (Your Actual)
```
backend/
  src/
    app.ts          ✅ (has /api/export)
    export.ts       ✅ (Pandoc service)
    routes/
      export.ts     ✅
frontend/
  src/
    components/
      ExportButtons.tsx  ⏳ NEXT
```

## Immediate Next Steps
1. Create ExportButtons.tsx
2. Test PDF generation from frontend
3. Add question bank UI
4. Connect to Postgres

## Tech Stack (Locked In)
- Frontend: React + Vite + Tailwind v4
- Backend: Node + Express + TypeScript
- Export: Pandoc + XeLaTeX
- DB: PostgreSQL + Prisma
- No changes needed - build on what works
