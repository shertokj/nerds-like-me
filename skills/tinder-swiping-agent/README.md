# Tinder Swiping Agent 💘

An AI agent skill that evaluates dating app profiles and makes structured swipe recommendations based on your personal preferences, dealbreakers, and green flags.

## What It Does

Instead of mindlessly swiping through hundreds of profiles, this skill gives you a repeatable decision framework. You describe a profile to the agent, and it returns a scored evaluation with a clear recommendation: Super Like, Right Swipe, Maybe, or Left Swipe — plus a personalized opening message for matches.

## Who It's For

- Anyone who uses Tinder, Hinge, Bumble, or similar dating apps
- People who want to be more intentional about their swiping
- Anyone who's ever spent 45 minutes swiping and realized they don't remember a single profile

## How It Works

1. **Set up your preferences** — Fill out the preference template in `references/my-preferences.md` with your dealbreakers, green flags, and what matters to you
2. **Describe a profile** — Tell the agent what you see: bio text, photo descriptions, age, distance, shared interests
3. **Get a recommendation** — The agent scores the profile, flags green/yellow signals, and gives you a clear swipe recommendation with reasoning
4. **Send a better opener** — For right swipes, the agent drafts a personalized opening message based on their actual profile

## Folder Structure

```
tinder-swiping-agent/
├── SKILL.md              # The core skill instructions
├── README.md             # You're reading this
├── examples/
│   ├── example-right-swipe.md    # Sample evaluation — right swipe
│   └── example-left-swipe.md     # Sample evaluation — left swipe
└── references/
    └── my-preferences.md         # Template for your personal preferences
```

## Setup

1. Copy this folder to your skills directory (`~/.openclaw/workspace/skills/` or `.claude/commands/`)
2. Edit `references/my-preferences.md` with your actual preferences
3. Start evaluating profiles!

## Example Usage

> "Evaluate this profile: Sarah, 28, 3 miles away. Bio says 'Dog mom, trail runner, terrible at cooking but great at ordering takeout.' Photos: hiking with a dog, at a brewery with friends, travel photo at Machu Picchu, candid laughing photo. Shared interests: hiking, dogs, craft beer."

The agent will return a structured evaluation with scoring, reasoning, and an opening message suggestion.

## Tips

- **Be honest in your preferences file.** The more accurate your dealbreakers and green flags, the better the recommendations.
- **Describe photos thoughtfully.** The agent can't see images, so your descriptions matter. "Group photo" is less useful than "group photo at a wedding, they're the one in blue."
- **Iterate on your preferences.** If you disagree with the agent's recommendations, update your preference file. It's a living document.
- **Use this as a gut-check, not a replacement for your judgment.** The agent helps you think through profiles more consistently, but your instincts still matter.

## Built at 🦞 Nerds Like Me — Agent Skill Hackathon, April 2026
