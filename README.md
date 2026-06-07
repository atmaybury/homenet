# homenet

## packages
 
  
 
 
Docker Compose setup for a self-hosted media server with VPN-protected torrenting.

## Services

| Service | Port | Description |
|---|---|---|
| [Gluetun](https://github.com/passteque/gluetun) | — | WireGuard VPN (ProtonVPN) with port forwarding |
| [qBittorrent](https://github.com/qbittorrent/qBittorrent) | 9091 | Torrent client (routed through VPN) |
| [Jellyfin](https://github.com/jellyfin/jellyfin) | 8096 | Media server |
| [Radarr](https://gihthub.com/Radarr/Radarr) | 7878 | Movie management |
| [Sonarr](https://github.com/Sonarr/Sonarr) | 8989 | TV management |
| [Homarr](https://github.com/homarr-labs/homarr) | 7575 | Dashboard |

## Setup

1. Clone the repo
2. Copy `.env.example` to `.env` and fill in your values
3. Run `docker compose up -d`

## Environment Variables

See `.env.example` for all required variables. Key ones:

- `WIREGUARD_PRIVATE_KEY` — from ProtonVPN dashboard → Downloads → WireGuard configuration
- `PUID` / `PGID` — run `id your_username` to get these
- `TZ` — timezone e.g. `Europe/London`
- `SECRET_ENCRYPTION_KEY` — random string for Homarr encryption

## Media Paths

Expects media on a single drive (required for hardlinking):

- `/mnt/8TBHDD/Movies`
- `/mnt/8TBHDD/TV`
- `/mnt/8TBHDD/Downloads`

## Notes

- qBittorrent and natmap share gluetun's network stack — all torrent traffic goes through the VPN
- Port forwarding is handled natively by gluetun and pushed to qBittorrent automatically
- Radarr/Sonarr hardlink completed downloads to media folders so seeding continues uninterrupted
