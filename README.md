# Zo Substrate

|
  Generalized Zo-to-Zo skill exchange system. Push and pull skills between any two Zo Computer
  instances using a shared GitHub repository as the substrate. Includes bundling with checksums,
  local context awareness, setup wizard, and dry-run support. Fully configurable — no hardcoded
  identities or repo URLs.

## Installation

```bash
cd /home/workspace/Skills
git clone https://github.com/vrijenattawar/zo-zo-substrate.git zo-substrate
python3 zo-substrate/bootloader.py
```

The bootloader will:
1. Survey your environment
2. Detect potential conflicts
3. Propose an installation plan
4. Execute only with your approval

## Required Secrets

Set these in **Zo Settings > Developers**:

- `ZO_WORKSPACE`
- `GITHUB_TOKEN`

## Configuration

```bash
cp config/settings.yaml.example config/settings.yaml
```

## License

MIT

---

Built for [Zo Computer](https://zo.computer).