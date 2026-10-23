# Security & SSDL Practices — FloodSiren

## Security Measures Implemented
* **Environment Secret Isolation:** All API keys and credentials are strictly kept inside `.env.local` files and ignored via `.gitignore`.
* **Database Authorization Rules:** Firebase Firestore security rules enforce write authorization and schema validation for incoming reports.
* **HTTPS Transport Security:** TLS encryption enforced across all web app endpoints via Vercel.
