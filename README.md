# Project Overview

Production Deploy on Telegram: @HarmonySocialBot

## Front-End
- **Framework**: React
- **Deployment**: [Netlify](https://hod1.netlify.app/) (Automatic deployment from `miniApp` branch)
- **Video Player**: User's viewing status is consistently tracked down every fraction of a second to ensure the user has indeed watched the video until the end to reward NIL points. Users must watch threshold (90%) of video duration to claim reward. If video is skipped (>3 seconds), watch time counter is halted.

## Back-End
- **Framework**: Express, Node.js, Axios
- **Deployment**: [Heroku](https://hod1-a52bc53a961e.herokuapp.com/) (Manual deployment with `git push heroku master`)
- **Components**: Includes both bot server and API server in `index.js`

### REST API Endpoints

- **GET /points**
  - **Parameters**: `userId`
  - **Description**: Retrieves the user's NIL balance (points).

- **GET /watch**
  - **Parameters**: `userId`, `videoId`
  - **Description**: Calls the function to mark a video as watched.

- **GET /watchedVideos**
  - **Parameters**: `userId`
  - **Description**: Retrieves the list of videos the user has watched.

- **POST /updateWatchedVideos**
  - **Parameters**: `userId`, `videoId`
  - **Description**: Updates the user's watched videos list.
 
- **GET /youtube/viewcount**
  - **Parameters**: `url`
  - **Description**: Fetches view count of specific youtube video from url

## Telegram MiniApp
- **Integration**: [Telegram MiniApp](https://t.me/HarmonyLotteryBot/hod1app)

# Tasks
- [ ] **Database**: Port user database from `index.js` server to an actual database.
- [x] **Video Player**: Implement a video player to embed YouTube videos when clicked on "watch" button.
- [x] **Verify watching video**: Implement a way to confirm the user has watched the video until the end, no skipping or just clicking on url.
- [x] Fix fastfowarding increasing watch time issue
- [ ] **UI Update**: Enhance the web UI for better visuals.--TBD
- [ ] **Video List Management**: Clean up and streamline the video list to allow updates from a single file.
- [ ] Add YouTube subscribe feature
- [ ] Reformat structure for 'tasks': currently a little awkward to have videos array inserted to index.js. Want to generalize for social tasks too.
- [ ] Maybe(?) move the user points to app bar not home.js
- [ ] Switch leaderboard from updating immediately (sorting takes time), update every hour or so and store it somewhere
- [ ] Further app improvement on storing data to cache instead of calling API every time
- [ ] Need to check how to prevent Netlify-side error when trying to reload link
- [x] Add referral code system
- [x] Add leaderboard for points
- [x] **Navigation Improvement**: Enhance the Telegram Mini App UI with navbars and appbars for better navigation.
- [x] Update bot details (change bot username)
- [x] Add inline keyboard menu button 'play'
- [x] Integrate Youtube API

# Notes
Previous testing stuff are stored on other branches (chat-based inetraction, lottery, etc)

# Instructions for replicating:
1. Install dependencies for both client and server:
```
npm i
```
2. Telegram: Create your bot with Telegram BotFather. Get API key, `touch .env` in `/server` (example given in .env.example). 
3. Server-side: Dpeloy to server-hosting or on local:
```
cd server
node index.js
```
4. Modify client-side API endpoint URLs in `client/App.js` with your PORT or deployed server URL.
5. Client-side: Deploy client side on hosting app. Make sure to add deploy setting `npm run build`. (Will need to be on hosting app, not local since need to connect through Telegram).
6. Give command to BotFather `/newapp` and register your Web App URL (front-end deploy link).
7. (Optional) Give command to BotFather `/setmenubutton`and give url (https://hod1.netlify.app/) to add menu button to bot.

