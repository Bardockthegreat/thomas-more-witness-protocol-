# Morus

**Tamper-proof witness record.**

Named for Thomas More (Latin: *Morus*), Lord Chancellor of England, executed 1535 because one man's fabricated testimony could not be disproven. Morus exists so that never happens again.

Two HTML files. No install. No account. No server. Works on any device with a browser.

---

## Files

| File | Purpose |
|------|---------|
| `witness.html` | Record and export a witness account |
| `review.html` | Review and compare accounts from multiple witnesses |

---

## How to use it

**To record:**
1. Open `witness.html` in any browser — Chrome, Firefox, Safari
2. Type what you witnessed. Press Record.
3. Repeat for each event.
4. Click Save records — write down the password shown — your file downloads.
5. Send the file to a lawyer, journalist, or trusted contact.
6. **Delete the file from your Downloads folder.** Then close the tab. The only remaining copy is the one you sent.

**To review multiple witnesses:**
1. Open `review.html`
2. Drop in `.morus` files from multiple witnesses
3. Enter the password for each file
4. Review the combined timeline
5. Export a report

**To verify a single file:**
1. Open `witness.html`
2. Click Verify a file
3. Drop in the `.morus` file, enter the password
4. The chain is recomputed and verified

---

## How it works

Everything stays on your device. Nothing is sent anywhere.

Each record is sealed with a cryptographic hash (SHA-256). Each record includes the hash of the one before it — so changing any entry breaks every entry that follows it.

When you save, the file is encrypted (AES-256-GCM) with your password, using 600,000 rounds of key stretching (PBKDF2-SHA256).

When you close the tab, all records vanish from your device. The only copy is the file you saved. **The export is the persistence. The user controls where it lives.**

---

## The .morus format

```json
{
  "morus":      "1.0",
  "enc":        "aes-256-gcm",
  "kdf":        "pbkdf2-sha256",
  "iterations": 600000,
  "salt":       "<hex>",
  "iv":         "<hex>",
  "data":       "<hex — ciphertext + GCM auth tag>",
  "count":      14,
  "created":    "<ISO 8601>"
}
```

Decrypted payload:

```json
{
  "entries": [
    { "seq": 1, "text": "...", "timestamp": "<ISO 8601>", "hash": "<SHA-256>" }
  ],
  "head":  "<final chain hash>",
  "count": 14
}
```

Hash chain: `entry.hash = SHA-256(JSON.stringify({ prev, seq, ts, text }))`

---

## Distribution

Both files are designed to be shared. Send them by email, Signal, USB drive, or QR code. They work on any device with a modern browser — Mac, Windows, Linux, Android, iOS.

The files are small by design. There is no app to install, no store to go through, no account required.

---

## The precedent

Phil Zimmermann built PGP in 1991, gave it away, and journalists in authoritarian countries still use it today. No company. No revenue. Just a format that outlasted everything around it.

Morus is built on the same principle. It is infrastructure, not a product. A standard, not a service.

---

## Author

BobbieB — *Blessed are the peacemakers: for they shall bee called the children of God.*

[@Bardockthegreat](https://github.com/Bardockthegreat)

---

## License

MIT. Do whatever you want with it. The only request: if you improve it, share it back.

---

## Contributing

The format specification is the most important thing to keep stable. If you build a compatible implementation in another language, open an issue — it belongs here.

Bug reports, security reviews, and translations are welcome.

---

*"The times are never so bad but that a good man can live in them."*
— Thomas More, 1535
