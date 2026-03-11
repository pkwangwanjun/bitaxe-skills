# AGENTS.md

This file provides guidance to Codex (Codex.ai/code) when working with code in this repository.

## Project Overview

This is a Codex skill for discovering and managing solo miners (Bitaxe and Nerd/NerdAxe devices) on a local network. The skill provides a CLI tool for scanning, inspecting, and configuring mining devices via their REST API.

## Key Commands

```bash
# Discover miners on the LAN
python3 scripts/solo_miner_tool.py discover --save /tmp/solo-miners.json

# Show specific device info
python3 scripts/solo_miner_tool.py show 192.168.28.89 --field bestSessionDiff

# Query raw JSON from device
python3 scripts/solo_miner_tool.py show luckyminer001 --format raw

# Update a setting and restart
python3 scripts/solo_miner_tool.py set luckyminer001 fanspeed=95 --restart

# Restart a device
python3 scripts/solo_miner_tool.py restart 192.168.4.1
```

## Architecture

- `SKILL.md` - Skill definition with usage workflow and field semantics
- `scripts/solo_miner_tool.py` - Main CLI tool (Python 3, standard library only)

## Device Types

- **Bitaxe**: Identified by keys `axeOSVersion`, `ipv4`, `boardVersion`
- **Nerd**: Identified by keys `deviceModel`, `hostip`, `hashRate_1d`, or nested `stratum.pools`

## API Endpoints

- `GET /api/system/info` - Discovery and reads
- `PATCH /api/system` - Update settings
- `POST /api/system/restart` - Restart device

## Reference

See `references/api-map.md` for the complete field mapping between Bitaxe/Nerd devices and normalized fields, plus writable settings allowlist.
