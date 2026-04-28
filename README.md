# ostrom-energy

Skill package for Ostrom spot-price automation.

It provides CLI commands to:
- Show upcoming hourly prices
- Find the cheapest contiguous charging/runtime window
- Trigger on/off commands from price thresholds

## Requirements

- Python 3
- Ostrom API credentials (`OSTROM_CLIENT_ID`, `OSTROM_CLIENT_SECRET`)

## Quick Start

```bash
cp .env.example .env
# edit .env with your credentials
bash run.sh prices --hours 24
```

## Common Commands

```bash
# Upcoming prices
bash run.sh prices --hours 36

# Cheapest 2-hour window
bash run.sh optimize --duration-hours 2

# Cheapest window for energy target (kWh / kW => duration)
bash run.sh optimize --kwh 28 --power-kw 11

# Dry-run control
bash run.sh control \
  --price-below 0.20 \
  --on-command "echo on" \
  --off-command "echo off"
```

## Safety

- `.env` is local-only and ignored by git.
- Keep control in dry-run first; only add `--execute` after validating thresholds.
- `--on-command`/`--off-command` run shell commands, so only use trusted command strings.

## Files

- `SKILL.md`: skill metadata and usage instructions
- `run.sh`: launcher that loads local env and executes Python script
- `ostrom_energy.py`: API + optimization/control logic
- `.env.example`: template for local secrets
