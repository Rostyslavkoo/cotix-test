# VueJs Developer Test

This is a Vue.js 3.x and TypeScript application developed using Vite.js. It fetches real-time track data from the provided JSON file and displays it on the web page. The page is updated every 2 seconds to show the current track being played and the history of past tracks.
## Design in Figma
https://www.figma.com/file/cq9BaWnzUJ5PuJSeWsPVFc/cotix-test?type=design&node-id=0%3A1&mode=design&t=8BXCUuG4ZNQUwHLi-1

***********************************
:warning: 
**Warning**

I had problems getting data from 'https://onair.radioapi.io/thisisgo/go/onair.json' via CORS, so if you also have this problem, you can use the Moesif Origin & CORS Changer custom extension
https://chrome.google.com/webstore/detail/moesif-origin-cors-change/digfbfaphojjndkpccljibejjbppifbc


Also, the api sometimes stop  changing the track that is currently playing, because of this it is impossible to make the startTime and progressBar for the track normally, if the api starts to change the track, then everything will work correctly
***********************************


## Task Requirements

1. Display all the tracks in the JSON file, with the "playing" item at the top, followed by the "history" items in reverse chronological order (most recent at the top, oldest at the bottom).
2. The "playing" item should include a progress bar indicating the playtime of the track.
3. Display the following details for each track item:
   - Title
   - Artist
   - Album (:interrobang: not found in api response)
   - ImageUrl (as an image)
   - Duration
   - StartTime (in the local time of the browser)

## How to Run the Application

1. Make sure you have Node.js and npm installed on your system. `(Node v16.3.0)`
2. Clone this repository to your local machine.
3. Navigate to the project directory using the terminal/command prompt.
4. Install the project dependencies using the following command:

```bash
npm install
```

5. Start the development server:

```bash
npm run dev
```

6. Open your browser and visit `http://localhost:5173` to view the application.

## Project Structure

The project follows a modular component-based structure to ensure easy integration into existing projects. Here's a brief overview of the project structure:

- `src/components/tracks`: Contains Vue components.
  - `tracksComponent.vue`: The main component that makes a request to the server, and does all the manipulations with the received data and distributes them to other components
  - `src/components/tracks/history`: Contains history components.
   - `historyComponent.vue`: Component to display the history list of  tracks.
   - `trackItem.vue`: Сomponent of detailed information in the story.
  - `src/components/tracks/playing`: Contains playing component.
   - `playingComponent.vue`: Component that shows the currently playing track 
   - `progressBar.vue`: Сomponent that displays a progress bar indicating the playback time of a track.
- `src/App.vue`: Main application component where the TrackList component is used.
- `src/main.ts`: Entry point of the application where Vue app is created and mounted to the DOM.
- `src/styles/`: Contains CSS files for styling the components.
- `vite.config.js`: Vite.js configuration file for project setup.

## Implementation Details

- Data fetching and updating are handled in the `tracksComponent` component.
- The playing track's progress bar is updated every 2 seconds.
- CSS styles are applied to achieve a clean and responsive layout.

## Additional Notes

- The code is optimized for performance and readability.
- Followed best practices in Vue.js development to ensure maintainability and extensibility.
