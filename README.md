# TMDb List Sorter

Do you ever wish you could sync your Plex movie library with a list on TMDb so that everyone could see what you have?

Do you ever wish that aformentioned TMDb list was color sorted to look aesthetically pleasing?

Well look no further! This script allows you to do just that!
---
Here's what you'll need:
- A Plex Token from your Plex library [Find out how to get one here](https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/).
- A Plex movie library.
- A TMDb API key [Find out how to get one here](https://developers.themoviedb.org/3/getting-started/introduction).
- A TMDb list
    - You'll need the ID for this list, which is the final integer in the list's URL.
- A Session ID
    - This script assumes that the user (that's mainly been me) has already generated a working session ID). If you haven't, simply change the line:
    ```python
    SESSION_ID = env['TMDB_SESSION_ID']
    ```
to either this:
```python
SESSION_ID = None
```
or this:
```python
SESSION_ID = ''
```

Doing so will activate the authentication sequence, which will redirect you to TMDb's page with a request token, and will generate a session ID for you.

---
How it works:

- Step 0 [optional]: Generate a `SESSION_ID` via the authentication sequence.
- Step 1: Extract TMDb IDs from Plex library.
- Step 2: Download the posters for every movie in your library.
- Step 3: Use K-Means clustering to identify the most dominant color in each poster.
- Step 4: Sort the list of movies by the dominant color in their poster.
- Step 5: Clears the TMDb list of all entries. This gives you a clean slate to work on.
- Step 6: Adds each movie to the TMDb list specified, sorted by the movie poster color.
