# Wordle+

A Unity-based clone of the popular word game **Wordle**, with a twist: play with **5-letter** or **6-letter** words instead of being limited to five. Built during the Wordle craze as a personal project and packaged as an Android app.

![Status](https://img.shields.io/badge/status-unreleased-orange) ![Unity](https://img.shields.io/badge/Unity-6000.4.1f1-black) ![Platform](https://img.shields.io/badge/platform-Android-brightgreen)

## About

Guess the hidden word in six tries. After each guess, the tiles change color to show how close you are:

- 🟩 **Green** — letter is in the word and in the correct spot
- 🟨 **Yellow** — letter is in the word but in the wrong spot
- ⬜ **Gray** — letter is not in the word

The on-screen keyboard mirrors these colors so you can track which letters you've already ruled in or out.

## Features

- **Multiple word lengths** — pick 5- or 6-letter rounds from the main menu
- **Random target word** pulled from a bundled dictionary each round
- **Dictionary validation** — guesses must be real words; invalid entries are flagged with a "Not a word" message
- **Hints** — reveal the first and last letter of the target word when you're stuck
- **Definition lookup** — after a round, jump to the Merriam-Webster definition of the target word
- **Win / lose summary screen** with retry and "change length" options
- **AdMob banner ads** integrated via the Google Mobile Ads SDK (currently using Google's test ad unit IDs)

## Project Structure

```
Assets/
├── Scripts/
│   ├── GameController.cs       Interface shared by all game modes
│   ├── FiveLetterGame.cs       5-letter game logic
│   ├── SixLetterGame.cs        6-letter game logic
│   ├── SevenLetterGame.cs      7-letter game logic (unfinished — no scene wired up)
│   ├── WordListGenerator.cs    Loads dictionaries from Resources at startup
│   ├── MainMenu.cs             Start-menu entry point
│   ├── ChooseWordMenu.cs       Word-length picker
│   ├── GameMenu.cs             In-game menu + AdMob banner
│   └── Box.cs                  Individual letter-tile behavior
├── Scenes/
│   ├── StartMenu.unity
│   ├── 5LetterGame.unity
│   └── 6LetterGame.unity
├── Resources/
│   ├── AllFiveLetterWords.txt
│   └── AllSixLetterWords.txt
├── Prefabs/                    Guess-row and menu prefabs
├── Sprites/                    Tile art + logo
├── Fonts/                      Bubblegum, Organic Relief (TMP)
└── Animations/                 "Not a word" toast
Builds/
└── Wordle+_v0.5.apk            Latest Android build
```

## Getting Started

### Prerequisites

- **Unity 6000.4.1f1** (Unity 6) — see [ProjectSettings/ProjectVersion.txt](ProjectSettings/ProjectVersion.txt)
- Android build support module (for producing APKs)

### Open the project

1. Clone this repo.
2. Open Unity Hub → **Add project from disk** → select the repo root.
3. Let Unity import packages (TextMesh Pro, Google Mobile Ads, External Dependency Manager).
4. Open `Assets/Scenes/StartMenu.unity` and press **Play**.

### Build for Android

1. `File → Build Profiles` → **Android** → *Switch Platform*.
2. Ensure `StartMenu`, `5LetterGame`, and `6LetterGame` are added to **Scenes in Build** in that order.
3. *Build* — the current shipped build lives at [Builds/Wordle+_v0.5.apk](Builds/).

## How to Play

1. Launch the app and tap **Play**.
2. Choose a word length (5 or 6).
3. Type guesses using the on-screen keyboard and press **Enter** to submit.
4. Use the **Hint** button if you're stuck — it reveals the first and last letter.
5. You have **6 attempts** to guess the word. Win or lose, you can tap the result screen to see the definition or start a new round.

## Known Limitations

- A 7-letter mode was scaffolded ([SevenLetterGame.cs](Assets/Scripts/SevenLetterGame.cs)) but never finished — there's no `7LetterGame` scene and no `AllSevenLetterWords.txt` word list, so `MainMenu.Awake` will throw if 7-letter generation runs against a missing resource.
- AdMob is configured with Google's **sample/test** ad unit IDs in [GameMenu.cs](Assets/Scripts/GameMenu.cs); replace with your own before publishing.
- Never fully polished for release — this was a "craze project."

## Credits

- **Developer:** Jarret Horner (Fryday Games)
- **Inspired by:** Josh Wardle's original *Wordle*
- **Ads:** Google Mobile Ads (AdMob) Unity SDK
- **Typography:** Bubblegum, Organic Relief (TextMesh Pro assets)
