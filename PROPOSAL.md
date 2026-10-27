# Hexfall (working title)

- [Description](#description)
- [Feature Milestones](#feature-milestones)
	* [Beta](#beta)
	* [Final](#final)
- [Stack](#stack)
- [Challenges](#challenges)

## Description

A daily strategy game played by the entire user population on a shared hexagonal grid
(some kind of mix of Wordle and Battleship?).

Each day, every player picks one hex to occupy and, optionally, one hex to attack.
Moves stay hidden until the daily cutoff, when the server resolves all of them at once:

- Occupying a hex grants **1000 points**.
- A successful attack grants **(players hit / participating players) × 1000** points.
- Being attacked deducts **(hits received / participating players) × 1000** points.
- A pacifist (no attack) hit by no more than 5% of participants earns a **750 point bonus**.

Each day applies a rotating modifier:

- Pacifist bonus is doubled.
- Attackers hit by more than 30% of participants lose 1.5× the usual points.
- Attacks also hit adjacent hexes.

Points add up into a weekly leaderboard that resets every week. After each resolution,
players can watch an animated replay of the day's results. Players have customizable profiles
with stats, a downloadable stat card, and shareable profile links. A Discord bot posts daily
results to a community server and answers stat queries.

## Feature Milestones

### Beta

- [ ] Local authentication and Discord OAuth
- [ ] Interactive hex map: select a hex to occupy and a hex to attack, then submit
- [ ] Daily resolution applying scoring rules and daily modifiers
- [ ] Weekly leaderboard with automatic weekly reset
- [ ] Basic profile page with game stats
- [ ] CI/CD pipeline deploying `main` to the VM automatically

### Final

- [ ] Animated daily results replay plus an archive of previous days
- [ ] Profile customization (profile picture, status line, about me)
- [ ] Stat card generation and download as a PNG
- [ ] Shareable profile links with generated preview images
- [ ] Discord bot: daily results posts and slash commands (`/stats`, `/leaderboard`, `/me`)
- [ ] Live online user count and submitted-move counters
- [ ] Localization (English and French), local-time display of the daily cutoff
- [ ] Rate limiting on authentication, move submission, and uploads

## Stack

Frontend:

- [ ] React + Vite (TypeScript)
- [ ] Tailwind CSS
- [ ] \(???\) for the hex map and replay (want fancy animations)
- [ ] \(???\) for stat card/image/media generation

Backend:

- [ ] Node.js + Express (TypeScript), RESTful API
- [ ] PostgreSQL
- [ ] WebSockets (live user counters and results notification)
- [ ] Discord API (OAuth and bot interactions)

Other:

- [ ] Docker + Docker Compose
- [ ] Nginx reverse proxy with HTTPS (Let's Encrypt)
- [ ] GitHub Actions + GitHub Container Registry

## Challenges

1. **Discord bot and OAuth**: Discord as OAuth provider, users can link their accounts
to Discord or create accounts using Discord directly. Linking to Discord with an existing
account should be possible. Additionally create a Discord bot that responds to slash commands
that it might see in a server. We'll have a server with this discord bot to provide Discord
users a way to partially interact with the app. The bot also posts daily results to the server
after resolving the current day's stats.
2. **Daily results replay**: Each resolution is stored and animated on the hex map.
Players can replay resolutions of the past few days.
3. **Stat card generation**: Stat cards are rendered server/client-side (idk) and are able to
be downloaded as images. Shared profile links also show generated preview images when posted
on social platforms.
4. **CI/CD**: Pushing to `main` and opening prs have tests run on them automatically.
Pushing to main deploys to VM automatically.
5. TODO
