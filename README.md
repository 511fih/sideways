# Sideways

A top-down 2D drift racer that runs in a single HTML file. Race AI opponents, chase your own ghost, and try to land on the high score boards.

## Features

- **Drift handling.** Hold Space to break traction and slide through corners. Skid marks stay on the track, and a drift-points counter runs while you slide.
- **AI opponents.** Race against 0 to 3 AI cars on Easy, Normal or Hard. Each driver has its own skill level and racing line, and the cars collide with each other.
- **Ghost racing.** Race a translucent replay of your fastest finished race, with a live time delta (green means you're ahead, red means you're behind).
- **High scores.** Top 5 fastest races and top 5 fastest laps, saved in your browser.
- **Touch controls** appear automatically on phones and tablets.

## Controls

| Action | Keyboard | Touch |
| --- | --- | --- |
| Accelerate | Up arrow or W | Gas |
| Brake and reverse | Down arrow or S | Brake |
| Steer | Left and right arrows, or A and D | Left and Right |
| Drift | Space | Drift |
| Respawn on track | R | |
| Back to menu | Esc | |

## Run it

There is no build step and nothing to install. Open `index.html` in a modern browser.

To serve it locally instead:

```sh
python3 -m http.server 8000
```

Then visit http://localhost:8000.

## Deploy with GitHub Pages

1. Put the game file in the root of your repo as `index.html`.
2. In the repo, open **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, then select your main branch and the `/ (root)` folder.
4. After a minute or so the game is live at `https://<your-username>.github.io/<repo-name>/`.

## How it works

- **Rendering:** Everything is drawn on one HTML canvas. The track and skid marks are rendered once to offscreen canvases and reused each frame.
- **Track:** A closed Catmull-Rom spline defines the racing line. The road, kerbs, and start line are drawn from it, and every car's position and lap progress are measured against it.
- **Physics:** A fixed 60 Hz step splits each car's velocity into forward and sideways parts. Sideways velocity is damped by a grip value, which the handbrake lowers to let the car slide.
- **AI:** Each AI car steers toward a point ahead on the racing line and brakes based on how sharp the upcoming corner is.
- **Ghost:** Your position and heading are recorded every physics step. Because the step is fixed, the replay stays in sync. The delta compares your time with the ghost's time at the same point on the track.

## Saved data

The ghost and high scores are stored in your browser's `localStorage` under the keys `sideways-ghost` and `sideways-scores`. They are specific to each browser and each site address, and clearing site data removes them.

## Credits

The page uses the [Big Shoulders Display](https://fonts.google.com/specimen/Big+Shoulders+Display) and [Barlow](https://fonts.google.com/specimen/Barlow) fonts from Google Fonts, both under the SIL Open Font License.

## License

Released under the [MIT License](LICENSE).
