# Sunfeld Domain Registry

Canonical mapping of all `*.sunfeld.nl` subdomains. Consult this before changing any domain references in code, nginx configs, or app settings.

All domains terminate SSL at **mc-proxy** (142.93.128.44) via wildcard Let's Encrypt cert, then proxy to internal services via Tailscale.

## Domain Map

| Domain | Service | Port | Host | Project Repo |
|--------|---------|------|------|-------------|
| `sunfeld.nl` | Sunfeld Landing Page | 9777 | vouwai | `sunfeld/sunfeld-landing` |
| `www.sunfeld.nl` | Redirect → sunfeld.nl | — | mc-proxy | — |
| `mc.sunfeld.nl` | Mission Control (master) | 9111 | vouwai | `sunfeld/mission-control` |
| `mc1.sunfeld.nl` | Mission Control Standalone (DOKS) | 443 | 129.212.220.252 | `sunfeld/mcs` |
| `fabio.sunfeld.nl` | MCS Tenant: Fabio (DOKS) | 443 | 129.212.220.252 | `sunfeld/mcs` |
| `editor.sunfeld.nl` | Video Editor (PWA + Android API) | 9444 | vouwai | `sunfeld/video-editor` |
| `vid.sunfeld.nl` | Video Hosting Service | 9555 | 129.212.220.252 (DOKS) | `sunfeld/video-host` |
| `video.sunfeld.nl` | Redirect → vid.sunfeld.nl | — | mc-proxy | — |
| `pefi.sunfeld.nl` | PEFI Investigation Platform | 3000 | vouwai | `sunfeld/pefi` |
| `fitness.sunfeld.nl` | Fitness App | 9333 | vouwai | — |
| `pgp.sunfeld.nl` | PGP Key Server | 9445 | vouwai | — |
| `llm.sunfeld.nl` | LLM Service | 4000 | vouwai | — |
| `condor.sunfeld.nl` | Condor News Scraper | 30849 | vouwai (k8s) | `sunfeld/competitor-and-news-scraper-condor` |
| `landing.sunfeld.nl` | Sunfeld Landing (alias) | 9777 | vouwai | `sunfeld/sunfeld-landing` |
| `sms.sunfeld.nl` | SMS Gateway | 3100 | vouwai | `sunfeld/sms-gateway-app` |
| `pp.sunfeld.nl` | PP Service | 9780 | vouwai | — |
| `pp1.sunfeld.nl` | PP Service (DOKS) | 443 | 129.212.220.252 | — |
| `ppai1.sunfeld.nl` | PP AI Service (DOKS) | 443 | 129.212.220.252 | — |
| `romulus.sunfeld.nl` | Romulus Italian Teacher Directory | 443 | 129.212.220.252 (DOKS) | `sunfeld/romulus` |
| `timeline.sunfeld.nl` | Timeline Service | 9778 | vouwai | — |
| `bitch-lasagna.sunfeld.nl` | Bitch Lasagna (prod) | 3000 | 129.212.220.252 (DOKS) | `sunfeld/bitch-lasagna` |
| `bitch-lasagna-dev.sunfeld.nl` | Bitch Lasagna (dev) | 3000 | 129.212.220.252 (DOKS) | `sunfeld/bitch-lasagna` |
| `assistant.sunfeld.nl` | Custom Android Assistant Backend (prod) | 8080 | 129.212.220.252 (DOKS) | `sunfeld/assistant` |
| `assistant-dev.sunfeld.nl` | Custom Android Assistant Backend (dev) | 8080 | 129.212.220.252 (DOKS) | `sunfeld/assistant` |

## Infrastructure

- **mc-proxy**: 142.93.128.44 (DigitalOcean droplet), Tailscale 100.124.239.5
- **vouwai**: 192.168.2.3, Tailscale 100.74.12.9 — runs all Docker containers
- **DOKS**: 129.212.220.252 — DigitalOcean Kubernetes (Amsterdam)
- **SSL**: Wildcard cert for `*.sunfeld.nl` via certbot DNS-01 (DigitalOcean)

## Rules

1. **Never swap domains between services** — each domain is permanently assigned to one service
2. **Always consult this registry** before changing domain references in code or configs
3. **Redirects** (video→vid, www→sunfeld.nl) are intentional — don't remove them
4. **Port assignments are fixed** — don't reassign ports without updating this registry
