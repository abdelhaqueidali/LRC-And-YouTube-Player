# LRC & YouTube Player (Project abandoned as many Youtube channels are set to not allow playing their videos from outside Youtube)

This project provides a simple web interface for playing YouTube videos synchronized with LRC lyrics files.  It allows users to select a song from a predefined list, load the corresponding LRC file, and display the lyrics in sync with the playing YouTube video.

## Live Demo

You can see a live demo of the project here: [https://abdelhaqueidali.github.io/LRC-And-YouTube-Player/](https://abdelhaqueidali.github.io/LRC-And-YouTube-Player/)

## Features

*   **Loads LRC Files:** Reads LRC (Lyric) files to display time-synchronized lyrics.
*   **YouTube Integration:** Embeds and plays YouTube videos using the YouTube Iframe API.
*   **Dynamic Song List:**  Fetches a list of songs and their associated YouTube links from a `data.txt` file.
*   **Lyric Synchronization:**  Highlights the current line of lyrics in sync with the YouTube video's playback time.
*   **Lyric Scrolling:** Automatically scrolls the lyrics to keep the current line in view.
*   **Lyric Seeking:**  Allows users to click on a lyric line to seek the YouTube video to that specific time.
*   **LRC Download:** Provides a button to download the currently loaded LRC file.
*   **Responsive Design:** Adapts to different screen sizes.
*   **Mobile Friendly Song Selection:**  Includes a "Show Song List" button to toggle the song list visibility, improving usability on smaller screens.
* **Plain Text Lyrics Extraction:** Easily copy plain text version of the lyrics.

## How It Works

1.  **Song List (data.txt):** The `data.txt` file contains a list of songs. Each line in this file represents a song and should be in the format `filename.lrc|youtube_link`.  The `filename.lrc` part specifies the name of the LRC file (located in the same directory as the HTML file), and `youtube_link` is the URL of the corresponding YouTube video.

    Example `data.txt`:

    ```
    Song1.lrc|https://www.youtube.com/watch?v=dQw4w9WgXcQ
    Song2.lrc|https://youtu.be/exampleVideoId
    ```

2.  **Loading the Song List:**  The JavaScript code fetches the `data.txt` file and parses it to create the song list displayed on the page. Each song in the list is a clickable element.

3.  **Loading a Song:** When a user clicks on a song in the list:
    *   The corresponding LRC file is fetched.
    *   The lyrics are parsed and displayed.
    *   The YouTube video is loaded using the provided YouTube link (extracting the video ID).
    *   The download button becomes visible.

4.  **LRC Parsing:** The `parseLRC` function converts the LRC file content into an array of JavaScript objects. Each object contains the `time` (in seconds) and the `text` of the lyric line.  The LRC format is expected to be: `[mm:ss.xx]lyric text`.

5.  **YouTube Player:** The YouTube Iframe API is used to embed and control the YouTube video. The API is loaded asynchronously.

6.  **Lyric Synchronization:**  The `syncLyrics` function is called repeatedly (every 100ms) while the video is playing.  It compares the current video time with the timestamps in the parsed LRC data to determine the currently playing lyric line.  The currently playing line is highlighted, and the lyrics container is scrolled to keep it in view.

7.  **Seeking:** Clicking on a lyric line calls the `seekTo` function, which uses the YouTube API to seek the video to the corresponding time.

8.  **Downloading:** The download button dynamically creates a link to download the LRC file as a text file.

## Setup and Usage

1.  **Clone the Repository:**
    ```bash
    git clone <repository_url>
    ```
    (Replace `<repository_url>` with the actual URL of your GitHub repository.)

2.  **Create `data.txt`:** Create a `data.txt` file in the same directory as your `index.html` file. Populate it with your song data as described above.

3.  **Create LRC Files:** Place your `.lrc` files in the same directory as `index.html`.  Make sure the filenames match those listed in `data.txt`.

4.  **Open `index.html`:** Open the `index.html` file in a web browser.

## Project Structure

*   **`index.html`:**  The main HTML file containing the structure of the webpage, the YouTube player, the lyrics display, and the JavaScript code.
*   **`data.txt`:**  A text file containing the list of songs, LRC filenames, and YouTube links.
*   **`.lrc` files:**  The lyric files (e.g., `Song1.lrc`, `Song2.lrc`).

## Dependencies

*   **YouTube Iframe API:**  Used for embedding and controlling the YouTube player.  The script is loaded dynamically within the `index.html`.

## Contributing
I welcome contributions! If you'd like to add features, improve the code, or fix bugs, please feel free to submit a pull request.
1. Fork this repo
2. Clone to you PC
3. Do your edits
4. Create a pull request

## Notes and Acknowledgements

*   The original concept and initial prompt were created by the owner of this repository.
*   The code was generated with the assistance of AI, specifically Claude Sonnet 3.5.
* This design focuses on sharing lyrics along with associated YouTube videos without hosting the song files directly, addressing copyright concerns and supporting content creators through ad revenue.
* The extracted lyrics from the LRC can be copied after selecting a song. If you want to get the lyrics in plain text, load the song and copy the lyrics from the lyrics section. To keep the timestamps with the lyrics, click on the "Download LRC" button and open the downloaded `.lrc` file with any text editor (e.g., Notepad++).
