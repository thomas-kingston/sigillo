# Sigillo — scheda tecnica

Sintesi di come funziona. Il rapporto completo (modello, dataset, esperimenti) è dell'autore
originale: [`report/rizzo-pii-report.pdf`](../report/rizzo-pii-report.pdf).

- **Modello:** mmBERT-base (ModernBERT), ~0,3 miliardi di parametri, classificazione di token
  su 22 tag; un 23° tag (URL) solo con regole. Gira su CPU, in ONNX.
- **Rete di regole:** controlli con checksum per IBAN (mod 97), carte (Luhn), codice fiscale e P.IVA.
- **Segnaposto reversibili:** ogni dato diventa `[TAG_n]`; il dizionario resta sul computer e si
  può disattivare.
- **OCR:** PaddleOCR-ONNX per scansioni e immagini; oscuramento vero dei PDF (PyMuPDF).
- **Server locale:** Flask su 127.0.0.1:5005; app desktop Tauri con sidecar Python.
- **Modello scaricato al primo avvio** da Hugging Face (versione e hash bloccati); disponibili
  installer offline.

## Limiti
Pseudonimizzazione, non anonimizzazione: circa l'1 % di dati può sfuggire. Metriche dichiarate
dall'autore, non verificate da terzi. Nessun audit indipendente.

## Licenze
Codice, modello e dataset: MIT © 2026 Simone Rizzo. Binari con PyMuPDF: AGPL-3.0.
