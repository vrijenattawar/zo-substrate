# Zo Substrate

Bidirectional skill exchange between any two [Zo Computer](https://zo.computer) instances, using a shared GitHub repository as the substrate.

Push skills from one Zo, pull them on another. Includes bundling with checksums, local context awareness, setup wizard, and full dry-run support.

## Architecture

```
Zo A                          GitHub Repo                  Zo B
┌──────────┐                 ┌──────────────┐              ┌──────────┐
│ Skills/  │  push           │ repo/Skills/ │  pull        │ Skills/  │
│ skill-x/ │ ──────────────► │  skill-x/    │ ◄─────────── │ skill-x/ │
│ skill-y/ │                 │  skill-y/    │              │ skill-y/ │
│          │                 │  MANIFEST    │              │          │
└──────────┘                 └──────────────┘              └──────────┘
```

## Installation

```bash
cd /home/workspace/Skills
git clone https://github.com/vrijenattawar/zo-substrate.git zo-substrate
pip install pyyaml
```

Or use the bootloader for guided installation:

```bash
python3 zo-substrate/bootloader.py
```

## Quick Start

```bash
# 1. Check prerequisites
python3 Skills/zo-substrate/scripts/substrate.py setup check

# 2. Initialize (creates config + optionally the shared GitHub repo)
python3 Skills/zo-substrate/scripts/substrate.py setup init \
  --identity my-zo \
  --partner their-zo \
  --repo myuser/our-substrate \
  --create-repo

# 3. Push skills
python3 Skills/zo-substrate/scripts/substrate.py push --dry-run
python3 Skills/zo-substrate/scripts/substrate.py push

# 4. On the other Zo: pull skills
python3 Skills/zo-substrate/scripts/substrate.py pull --dry-run
python3 Skills/zo-substrate/scripts/substrate.py pull

# 5. Check status
python3 Skills/zo-substrate/scripts/substrate.py status
```

## Commands

| Command | Description |
|---------|-------------|
| `push [--skills x,y] [--dry-run]` | Push skills to the substrate repo |
| `pull [--skills x,y] [--dry-run] [--verbose]` | Pull skills from the substrate repo |
| `status` | Show last push/pull, discoverable skills |
| `setup check` | Verify prerequisites (git, gh, auth) |
| `setup init --identity ... --partner ... --repo ...` | Create config |
| `bundle create <skill>` | Create a tarball bundle with checksums |
| `bundle validate <path>` | Validate a bundle |
| `bundle list` | List discoverable skills |
| `context refresh` | Scan workspace and save context snapshot |
| `context query [--what summary\|skills\|structure\|json]` | Query context |

## Configuration

After `setup init`, your config lives at `config/substrate.yaml`:

```yaml
identity:
  name: "my-zo"
  handle: "myhandle.zo.computer"

partner:
  name: "their-zo"
  handle: "theirhandle.zo.computer"

substrate:
  repo: "username/substrate-repo"
  branch: "main"
  clone_method: "https"

export:
  skills: []          # Empty = auto-detect all skills with SKILL.md
  auto_detect: true
  exclude:
    - "zo-substrate"  # Don't export yourself

pull:
  install_dir: "Skills"
  backup_existing: true
```

## Requirements

- Python 3.9+
- PyYAML (`pip install pyyaml`)
- Git 2.30+
- GitHub CLI (`gh`) — for repo creation
- `GITHUB_TOKEN` in environment or `gh auth login` completed

## Safety

- **Push** never modifies the local workspace
- **Pull** backs up existing skills before overwriting (configurable)
- **Dry-run** support on all mutating commands
- **MANIFEST.json** tracks provenance (who pushed, when, what SHA)
- All operations logged to `substrate.log`

## License

MIT

---

Built for [Zo Computer](https://zo.computer).
