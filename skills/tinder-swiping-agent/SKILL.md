---
name: tinder-swiping-agent
description: >
  Evaluates Tinder profiles and makes swipe decisions (left/right/super-like)
    based on user-defined preferences and dealbreakers. Takes a profile summary
      (bio text, photos description, age, distance, shared interests) and outputs
        a structured swipe recommendation with reasoning. Use when the user says
          "evaluate this profile," "should I swipe right," "rate this match,"
            or "help me decide on this person."
            ---

            # Tinder Swiping Agent

            Evaluates dating app profiles against your personal preferences and outputs a
            structured swipe recommendation with clear reasoning. Turns your "gut feel"
            into a repeatable, consistent decision framework so you stop stress-swiping
            at 1 AM.

            ## Input

            The user provides profile details from a Tinder (or similar dating app) profile.
            These may include any combination of:

            - **Bio text** — the person's written bio / about me
            - **Photo descriptions** — what you see in their photos (since the agent can't see images, describe them: "hiking photo, group photo with friends, dog pic, mirror selfie")
            - **Age** — their listed age
            - **Distance** — how far away they are
            - **Shared interests** — any interests or tags Tinder shows as shared
            - **Prompts/answers** — any prompt responses (e.g., "My simple pleasures: coffee and sunsets")
            - **Dealbreakers spotted** — anything obvious the user flags ("they smoke," "they said they hate dogs")

            The user should also have previously set up their **preference profile** (see the
            `references/my-preferences.md` file for a template). If no preference file exists,
            use reasonable defaults and ask the user to fill one out for better results.

            ## Steps

            1. **Parse the profile.** Extract all available signals: bio text, photo vibe,
               age, distance, shared interests, prompt answers, and any red/green flags.

               2. **Check dealbreakers first.** Compare against the user's dealbreaker list.
                  If ANY dealbreaker is present, recommend LEFT SWIPE immediately and explain
                     which dealbreaker was triggered. Do not continue scoring.

                     3. **Score green flags.** Check the profile against the user's green flag list.
                        Award points for each match:
                           - Strong match (directly stated): +3
                              - Moderate match (implied or likely): +2  
                                 - Weak match (possible but uncertain): +1

                                 4. **Score yellow flags.** Check for items on the user's caution list.
                                    Deduct points:
                                       - Minor concern: -1
                                          - Moderate concern: -2

                                          5. **Assess photo vibe.** Based on photo descriptions, evaluate:
                                             - Effort level (curated vs. lazy)
                                                - Lifestyle compatibility signals
                                                   - Authenticity indicators (all group photos = hard to tell who they are)

                                                   6. **Calculate recommendation.** Based on total score:
                                                      - Score 8+: SUPER LIKE — strong match, go for it
                                                         - Score 5-7: RIGHT SWIPE — solid match, worth a conversation
                                                            - Score 2-4: MAYBE — could go either way, swipe right if you're feeling generous
                                                               - Score 0-1: LEFT SWIPE — not enough signal, probably not a match
                                                                  - Negative score: LEFT SWIPE — yellow flags outweigh the good

                                                                  7. **Draft an opening message.** If the recommendation is RIGHT SWIPE or SUPER LIKE,
                                                                     draft a short, personalized opening message (under 50 words) referencing something
                                                                        specific from their profile. No generic "hey" messages.

                                                                        ## Output Format

                                                                        ```
                                                                        ## Profile Evaluation

                                                                        **Name/Age:** [Name], [Age]
                                                                        **Distance:** [X] miles away

                                                                        ### Dealbreaker Check
                                                                        [PASS ✅ or FAIL ❌ — if fail, state which dealbreaker and stop here]

                                                                        ### Green Flags 🟢
                                                                        - [Flag]: [reason] (+X)
                                                                        - [Flag]: [reason] (+X)

                                                                        ### Yellow Flags 🟡
                                                                        - [Flag]: [reason] (-X)

                                                                        ### Photo Vibe
                                                                        [1-2 sentence assessment of their photos]

                                                                        ### Score: [X] / 10

                                                                        ### Recommendation: [SUPER LIKE ⭐ | RIGHT SWIPE 👉 | MAYBE 🤷 | LEFT SWIPE 👈]

                                                                        **Reasoning:** [2-3 sentence summary of why]

                                                                        ### Suggested Opening Message
                                                                        > [Your personalized opener here]
                                                                        ```

                                                                        ## Rules

                                                                        - Never invent profile details that weren't provided — if info is missing, note it as "[not provided]" and factor the uncertainty into scoring
                                                                        - Keep the total evaluation under 300 words
                                                                        - Be honest but not mean — these are real people; frame yellow flags as compatibility concerns, not insults
                                                                        - If the user hasn't set up preferences yet, use these defaults: look for effort in bio, shared interests, photos that show personality, and flag very low-effort profiles
                                                                        - The opening message must reference something specific from their profile — no generic openers
                                                                        - If ALL photos are group photos and you can't tell who the person is, flag this as a yellow flag (-2)
                                                                        - Profiles with zero bio text get an automatic -2 penalty (low effort)
                                                                        - Super Like recommendations should be rare — reserve for genuinely strong matches (score 8+)
                                                                        - Never make assumptions about someone's character based on appearance descriptions alone — focus on behavioral signals (effort, interests, lifestyle indicators)
                                                                        - If the user says "just swipe right on everyone," gently push back and explain that being selective leads to better matches
