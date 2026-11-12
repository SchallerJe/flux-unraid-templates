# Flux-Server – Unraid template

Unraid (dockerMan / Community Applications format) template for the **Flux server**, the backend of the Flux 3D-print cockpit app.

> Closed beta, proprietary image, linux/amd64 only. The companion iOS app is distributed via TestFlight. Info: https://flux.derdrucktschonwieder.com

## Installation (English)

1. **Prepare the appdata folder** (Unraid terminal). The container runs as UID 1000 (`node`), while Unraid creates folders as `nobody` (99:100). Without this step the server cannot save anything:
   ```bash
   mkdir -p /mnt/user/appdata/flux-server
   chown -R 1000:1000 /mnt/user/appdata/flux-server
   ```
2. Unraid: **Docker** > **Template Repositories** (bottom of the page), add this line and save:
   `https://github.com/SchallerJe/flux-unraid-templates`
   (placeholder, the repository is not published yet)
3. **Add Container**, pick the template **Flux-Server**. Defaults are fine for a LAN setup (host port 3021). Behind a reverse proxy set *Local pairing* to `false`.
4. **Apply.** Wait until the container runs.
5. **Setup token:** click the container icon > **Logs** and look for `Setup token` (looks like `7K2QX-9M4VD-BH3TN`).
6. Click the container icon > **WebUI**, enter the token, accept the beta terms and press *Claim this server*. The setup assistant then guides you through printers and app pairing.

Updates: container icon > *Force update* (or the usual Unraid update check). Back up the appdata folder: it contains your secrets (`secrets.json`).

## Installation (Deutsch)

1. **appdata-Ordner vorbereiten** (Unraid-Terminal). Der Container läuft als UID 1000 (`node`), Unraid legt Ordner als `nobody` (99:100) an. Ohne diesen Schritt kann der Server nichts speichern:
   ```bash
   mkdir -p /mnt/user/appdata/flux-server
   chown -R 1000:1000 /mnt/user/appdata/flux-server
   ```
2. Unraid: **Docker** > **Template Repositories** (unten auf der Seite), diese Zeile eintragen und speichern:
   `https://github.com/SchallerJe/flux-unraid-templates`
   (Platzhalter, das Repository ist noch nicht veröffentlicht)
3. **Add Container**, Vorlage **Flux-Server** wählen. Für das Heimnetz passen die Standardwerte (Host-Port 3021). Hinter einem Reverse Proxy *Local pairing* auf `false` setzen.
4. **Apply** und warten, bis der Container läuft.
5. **Setup-Token:** Container-Icon > **Logs**, nach `Setup token` suchen (sieht aus wie `7K2QX-9M4VD-BH3TN`).
6. Container-Icon > **WebUI**, Token eingeben, Beta-Bedingungen bestätigen, *Server übernehmen*. Der Einrichtungsassistent führt durch Drucker und App-Kopplung.

Updates: Container-Icon > *Force update*. Den appdata-Ordner sichern: Er enthält deine Schlüssel (`secrets.json`).

## Settings

| Variable | Purpose |
|---|---|
| `TZ` | Timezone for logs |
| `FLUX_LOCAL_PAIRING` | LAN pairing requests (default `true`; `false` behind proxy) |
| `FLUX_PUSH_RELAY` | `off` forbids the push relay |
| `FLUX_PUSH_RELAY_INVITE` | Relay invitation code (secret, optional) |
| `FLUX_PUBLIC_URL` | Public URL behind a reverse proxy |
| `FLUX_TRUST_PROXY` | Number of reverse proxies |
| `FLUX_COOKIE_SECURE` | Force Secure session cookie |
| `FLUX_API_KEY`, `SESSION_SECRET` | Optional, auto-generated if empty |
| `ANTHROPIC_API_KEY` | Own key for the AI label scan (optional) |

## License

See [LICENSE-NOTE.md](LICENSE-NOTE.md).
