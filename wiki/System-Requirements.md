# System Requirements

Before installing CVAT, make sure the machine that will act as the server meets the requirements below. Annotators only need a computer with Google Chrome — they do not need to install anything.

---

## Server Machine (where CVAT is installed)

### Minimum Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| CPU | 4 cores | 8+ cores |
| RAM | 8 GB | 16 GB or more |
| Disk space | 50 GB free | 200 GB+ (depends on video volume) |
| Operating system | Ubuntu 20.04 / 22.04 (recommended), Windows 10 with WSL2, or macOS | Ubuntu 22.04 LTS |
| Internet connection | Required during installation | Not required after setup |

### For AI-Assisted Annotation (Segment Anything Model)

Running AI models locally requires additional resources:

| Component | CPU-only | With GPU (recommended) |
|-----------|----------|------------------------|
| RAM | 16 GB | 16 GB |
| GPU | Not required | NVIDIA GPU with 8 GB+ VRAM (e.g. RTX 3080, A10) |
| NVIDIA drivers | Not required | 525+ (for CUDA 12) |
| CUDA | Not required | 11.7 or 12.x |

> **Note:** AI annotation works on CPU but will be noticeably slower (several seconds per frame rather than under a second). For routine clinical annotation sessions a GPU is strongly recommended.

---

## Software Requirements (Server)

| Software | Minimum version | Notes |
|----------|----------------|-------|
| Docker Engine | 20.10 | Installed as part of the installation guide |
| Docker Compose plugin | 2.0 | Included with Docker Engine on Ubuntu |
| Git | 2.x | For cloning the CVAT repository |
| Google Chrome | Latest stable | On the server or any annotator machine |

---

## Annotator Machines (clinician workstations)

Annotators access CVAT through a browser. No local software installation is needed beyond the browser.

| Requirement | Details |
|-------------|---------|
| Browser | **Google Chrome** (required — other browsers are not fully supported) |
| Display resolution | 1920 × 1080 or higher recommended |
| Network | Must be able to reach the server's IP address and port 8080 |
| Mouse | Standard mouse required; a mouse with a scroll wheel is recommended |

---

## Network Setup

- CVAT runs on **port 8080** by default.
- If annotators are on the same local network as the server, you typically only need to share the server's local IP address (e.g. `http://192.168.1.50:8080`).
- If annotators need to access the server over the internet, the administrator will need to configure appropriate firewall rules and ideally set up HTTPS (see the installation guide).

---

## Next Step

Proceed to the installation guide for your operating system:

- [Installation — Ubuntu](Installation-Ubuntu) *(recommended)*
- [Installation — Windows](Installation-Windows)
- [Installation — macOS](Installation-macOS)
