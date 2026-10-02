# YouTube Deep Tutor

Turns a long educational video into a course that teaches it back to you one
concept at a time, and keeps an honest record of what you actually understood.

It is one markdown file. There is nothing to run and nothing to sign up for.

## What it does

1. Takes a YouTube URL.
2. Transcribes the video through the Gemini API, which reads public YouTube
   videos directly. It does not scrape the page or search the web for a summary.
3. Audits that transcript before teaching anything: checks for truncation,
   compares the range it processed against the real duration, and marks passages
   it could not hear or read rather than filling them with a plausible guess.
4. Builds a map of every substantive concept in the video, with a stable ID,
   its source timestamps, its prerequisites, and whether the source for it is
   available, partial or missing.
5. Teaches one concept per turn and ends with one question, then stops and waits.

## The part that makes it different

It keeps three things apart and never merges them:

- source actually read
- concept actually taught
- understanding actually shown

Typing "okay" or "next" does not fill the third column. Neither does watching an
explanation. It takes your own words on a question you had not seen. If you can
repeat an idea back correctly but cannot use it on a new case, the record says
recall, not application, and says so to your face.

Most study tools collapse those three into one progress bar. A progress bar only
proves a paragraph got printed.

## Install

### Claude Code

Save `youtube-deep-tutor.md` to `~/.claude/commands/`, then run:

```
/youtube-deep-tutor https://www.youtube.com/watch?v=...
```

### Claude, ChatGPT, or anything else with a chat box

Paste the contents of `youtube-deep-tutor.md` as a project instruction, a custom
GPT instruction, or just as your first message, then send the URL. The file is
plain prose, not code, so it works anywhere a long instruction is accepted.

## You need your own Gemini API key

Stated plainly, because it is the one thing that will stop you.

Get a free key at https://aistudio.google.com/apikey and set it:

```
export GEMINI_API_KEY=your_key_here
```

Put that in your shell profile so it survives a new terminal. Google's free tier
covers normal use. The skill reads the key from the environment and will not ask
you to paste it into a chat.

No key, no transcript. You can still use it by pasting a transcript yourself, and
it will tell you plainly that it is working from your text rather than from the
video, which is not the same thing.

## What it will not do

- It will not pretend to have read a video it could not read. If the Gemini call
  fails, hits a quota, or the video is private or too long, it says which of
  those happened and stops.
- It will not treat a model-generated transcript as verified human captions. The
  timings are estimates and it labels them that way.
- It will not invent a screenshot, a diagram, or a number that was never in the
  source.
- It will not give you a summary. That is a different tool.

## Licence

MIT. Take it, change it, ship it.
